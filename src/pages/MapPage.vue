<template>
  <q-page class="page map-page">
    <div class="topbar">
      <router-link to="/" class="brand-link"><span>Kanu Systems</span></router-link>
      <nav class="desktop-nav">
        <router-link to="/about">Method</router-link>
        <router-link to="/map">Live Map</router-link>
      </nav>
      <button type="button" class="theme-toggle" @click="toggleTheme">Theme</button>
    </div>

    <div class="map-header">
      <div class="map-title">
        <div class="eyebrow">Geospatial Operations</div>
        <h1>Kenya County Map</h1>
        <p class="sub">Interactive county boundaries rendered from the HUMDATA GeoJSON dataset.</p>
      </div>
      <router-link class="back-link" to="/">Return home</router-link>
    </div>

    <div class="page-layout">
      <div class="left-panel">
        <div class="county-selector">
          <h2>Select County</h2>
          <ul class="county-list">
            <li v-for="(countyName, index) in countyNames" :key="countyName">
              <button
                type="button"
                :class="{ active: index === selectedCountyIndex }"
                @click="selectCounty(index)"
              >
                {{ countyName }}
              </button>
            </li>
          </ul>
        </div>

        <div v-if="selectedCounty" class="county-details">
          <div class="detail-section">
            <h3>{{ selectedCounty.properties.name }}</h3>
            <p class="detail-row"><strong>Code:</strong> {{ selectedCounty.properties.code }}</p>
            <p class="detail-row">
              <strong>Capital:</strong> {{ selectedCounty.properties.capital }}
            </p>
          </div>
          <div class="detail-section">
            <h4>Sub-Counties</h4>
            <ul class="sub-county-list">
              <li v-for="(subCounty, idx) in selectedCounty.properties.sub_counties" :key="idx">
                <button
                  type="button"
                  :class="{ active: idx === selectedSubCountyIndex }"
                  @click="selectSubCounty(idx)"
                >
                  {{ subCounty }}
                </button>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <div class="map-container">
        <svg id="mapSvg" viewBox="0 0 700 600"></svg>
        <div id="tooltip"></div>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { geoMercator, geoPath, groups, json, select } from 'd3'
import { onMounted, ref } from 'vue'
import geojsonUrl from 'src/stores/ken_admin2.geojson?url'

const toggleTheme = () => {
  const isSoft = document.body.classList.toggle('theme-soft')
  document.body.classList.toggle('theme-dark', !isSoft)
  document.body.classList.toggle('body--dark', !isSoft)
  document.body.classList.toggle('body--light', isSoft)
  document.body.style.setProperty('--q-dark-page', isSoft ? '#faf8f6' : '#07110a')
}

// Full rich county metadata.
// The map will use this to attach capital, code, and sub-county details.
const richCountyData = [
  {
    name: 'Mombasa',
    code: '001',
    capital: 'Mombasa',
    sub_counties: ['Changamwe', 'Jomvu', 'Kisauni', 'Nyali', 'Likoni', 'Mvita'],
  },
  {
    name: 'Kwale',
    code: '002',
    capital: 'Kwale',
    sub_counties: ['Msambweni', 'Lungalunga', 'Kwale', 'Kinango'],
  },
  {
    name: 'Kilifi',
    code: '003',
    capital: 'Kilifi',
    sub_counties: ['Bahari', 'Kilifi South', 'Kaloleni', 'Rabai', 'Ganze', 'Malindi', 'Magarini'],
  },
  { name: 'Tana River', code: '004', capital: 'Hola', sub_counties: ['Garsen', 'Galole', 'Bura'] },
  { name: 'Lamu', code: '005', capital: 'Lamu', sub_counties: ['Lamu East', 'Lamu West'] },
  {
    name: 'Taita-Taveta',
    code: '006',
    capital: 'Mwatate',
    sub_counties: ['Taveta', 'Wundanyi', 'Mwatate', 'Voi'],
  },
  {
    name: 'Garissa',
    code: '007',
    capital: 'Garissa',
    sub_counties: ['Garissa', 'Balambala', 'Lagdera', 'Dadaab', 'Fafi', 'Ijara'],
  },
  {
    name: 'Wajir',
    code: '008',
    capital: 'Wajir',
    sub_counties: ['Wajir North', 'Wajir East', 'Wajir South', 'Wajir West', 'Eldas', 'Tarbaj'],
  },
  {
    name: 'Mandera',
    code: '009',
    capital: 'Mandera',
    sub_counties: [
      'Mandera West',
      'Mandera North',
      'Mandera Central',
      'Mandera East',
      'Mandera South',
      'Banisa',
    ],
  },
  {
    name: 'Marsabit',
    code: '010',
    capital: 'Marsabit',
    sub_counties: ['Moyale', 'North Horr', 'Saku', 'Laisamis'],
  },
  {
    name: 'Isiolo',
    code: '011',
    capital: 'Isiolo',
    sub_counties: ['Isiolo', 'Merti', 'Garba Tulla'],
  },
  {
    name: 'Meru',
    code: '012',
    capital: 'Meru',
    sub_counties: [
      'Igembe South',
      'Igembe Central',
      'Igembe North',
      'Tigania West',
      'Tigania East',
      'Imenti North',
      'Buuri',
      'Imenti Central',
      'Imenti South',
    ],
  },
  {
    name: 'Tharaka-Nithi',
    code: '013',
    capital: 'Chuka',
    sub_counties: ['Maara', 'Chuka', 'Tharaka'],
  },
  {
    name: 'Embu',
    code: '014',
    capital: 'Embu',
    sub_counties: ['Manyatta', 'Runyenjes', 'Mbeere North', 'Mbeere South'],
  },
  {
    name: 'Kitui',
    code: '015',
    capital: 'Kitui',
    sub_counties: [
      'Mwingi North',
      'Mwingi Central',
      'Mwingi South',
      'Kitui West',
      'Kitui Central',
      'Kitui Rural',
      'Kitui South',
      'Kitui East',
    ],
  },
  {
    name: 'Machakos',
    code: '016',
    capital: 'Machakos',
    sub_counties: [
      'Masinga',
      'Yatta',
      'Kangundo',
      'Matungulu',
      'Kathiani',
      'Mavoko',
      'Machakos Town',
      'Mwala',
    ],
  },
  {
    name: 'Makueni',
    code: '017',
    capital: 'Wote',
    sub_counties: ['Mbooni', 'Kaiti', 'Makueni', 'Kibwezi West', 'Kibwezi East', 'Kilome'],
  },
  {
    name: 'Nyandarua',
    code: '018',
    capital: 'Ol Kalou',
    sub_counties: ['Kinangop', 'Kipipiri', 'Ol Kalou', 'Ol Joro Orok', 'Ndaragwa'],
  },
  {
    name: 'Nyeri',
    code: '019',
    capital: 'Nyeri',
    sub_counties: ['Tetu', 'Kieni', 'Mathira', 'Othaya', 'Mukurweini', 'Nyeri Town'],
  },
  {
    name: 'Kirinyaga',
    code: '020',
    capital: 'Kerugoya',
    sub_counties: ['Mwea', 'Gichugu', 'Ndia', 'Kirinyaga Central'],
  },
  {
    name: "Murang'a",
    code: '021',
    capital: "Murang'a",
    sub_counties: ['Kangema', 'Mathioya', 'Kiharu', 'Kigumo', 'Maragua', 'Kandara', 'Gatanga'],
  },
  {
    name: 'Kiambu',
    code: '022',
    capital: 'Kiambu',
    sub_counties: [
      'Gatundu South',
      'Gatundu North',
      'Githunguri',
      'Ruiru',
      'Juja',
      'Thika Town',
      'Kiambu',
      'Limuru',
      'Kikuyu',
      'Kabete',
      'Lari',
    ],
  },
  {
    name: 'Turkana',
    code: '023',
    capital: 'Lodwar',
    sub_counties: [
      'Turkana North',
      'Turkana West',
      'Turkana Central',
      'Loima',
      'Turkana South',
      'Turkana East',
    ],
  },
  {
    name: 'West Pokot',
    code: '024',
    capital: 'Kapenguria',
    sub_counties: ['Kapenguria', 'Sigor', 'Kacheliba', 'Pokot South'],
  },
  {
    name: 'Samburu',
    code: '025',
    capital: 'Maralal',
    sub_counties: ['Samburu North', 'Samburu East', 'Samburu West'],
  },
  {
    name: 'Trans-Nzoia',
    code: '026',
    capital: 'Kitale',
    sub_counties: ['Kwanza', 'Endebess', 'Saboti', 'Kiminini', 'Cherangany'],
  },
  {
    name: 'Uasin Gishu',
    code: '027',
    capital: 'Eldoret',
    sub_counties: ['Soy', 'Turbo', 'Moiben', 'Ainabkoi', 'Kapseret', 'Kesses'],
  },
  {
    name: 'Elgeyo-Marakwet',
    code: '028',
    capital: 'Iten',
    sub_counties: ['Marakwet East', 'Marakwet West', 'Keiyo North', 'Keiyo South'],
  },
  {
    name: 'Nandi',
    code: '029',
    capital: 'Kapsabet',
    sub_counties: ['Tinderet', 'Aldai', 'Nandi Hills', 'Chesumei', 'Emgwen', 'Mosop'],
  },
  {
    name: 'Baringo',
    code: '030',
    capital: 'Kabarnet',
    sub_counties: [
      'Tiaty',
      'Baringo North',
      'Baringo Central',
      'Baringo South',
      'Mogotio',
      'Eldama Ravine',
    ],
  },
  {
    name: 'Laikipia',
    code: '031',
    capital: 'Rumuruti',
    sub_counties: ['Laikipia North', 'Laikipia East', 'Laikipia West'],
  },
  {
    name: 'Nakuru',
    code: '032',
    capital: 'Nakuru',
    sub_counties: [
      'Molo',
      'Njoro',
      'Naivasha',
      'Gilgil',
      'Kuresoi South',
      'Kuresoi North',
      'Subukia',
      'Rongai',
      'Bahati',
      'Nakuru West',
      'Nakuru East',
    ],
  },
  {
    name: 'Narok',
    code: '033',
    capital: 'Narok',
    sub_counties: [
      'Narok North',
      'Narok South',
      'Narok West',
      'Narok East',
      'Kilgoris',
      'Emurua Dikirr',
    ],
  },
  {
    name: 'Kajiado',
    code: '034',
    capital: 'Kajiado',
    sub_counties: [
      'Kajiado North',
      'Kajiado Central',
      'Kajiado East',
      'Kajiado West',
      'Kajiado South',
    ],
  },
  {
    name: 'Kericho',
    code: '035',
    capital: 'Kericho',
    sub_counties: ['Kipkelion East', 'Kipkelion West', 'Ainamoi', 'Bureti', 'Belgut', 'Sigowet'],
  },
  {
    name: 'Bomet',
    code: '036',
    capital: 'Bomet',
    sub_counties: ['Sotik', 'Chepalungu', 'Bomet East', 'Bomet Central', 'Konoin'],
  },
  {
    name: 'Kakamega',
    code: '037',
    capital: 'Kakamega',
    sub_counties: [
      'Lugari',
      'Likuyani',
      'Malava',
      'Lurambi',
      'Navakholo',
      'Mumias West',
      'Mumias East',
      'Matungu',
      'Butere',
      'Khwisero',
      'Shinyalu',
      'Ikolomani',
    ],
  },
  {
    name: 'Vihiga',
    code: '038',
    capital: 'Vihiga',
    sub_counties: ['Vihiga', 'Sabatia', 'Hamisi', 'Luanda', 'Emuhaya'],
  },
  {
    name: 'Bungoma',
    code: '039',
    capital: 'Bungoma',
    sub_counties: [
      'Mt. Elgon',
      'Sirisia',
      'Kabuchai',
      'Bumula',
      'Kanduyi',
      'Webuye East',
      'Webuye West',
      'Kimilili',
      'Tongaren',
    ],
  },
  {
    name: 'Busia',
    code: '040',
    capital: 'Busia',
    sub_counties: [
      'Teso North',
      'Teso South',
      'Nambale',
      'Matayos',
      'Butula',
      'Funyula',
      'Budalangi',
    ],
  },
  {
    name: 'Siaya',
    code: '041',
    capital: 'Siaya',
    sub_counties: ['Ugenya', 'Ugunja', 'Alego Usonga', 'Gem', 'Bondo', 'Rarieda'],
  },
  {
    name: 'Kisumu',
    code: '042',
    capital: 'Kisumu',
    sub_counties: [
      'Kisumu West',
      'Kisumu Central',
      'Kisumu East',
      'Seme',
      'Nyando',
      'Muhoroni',
      'Nyakach',
    ],
  },
  {
    name: 'Homa Bay',
    code: '043',
    capital: 'Homa Bay',
    sub_counties: [
      'Kasipul',
      'Kabondo',
      'Karachuonyo',
      'Rangwe',
      'Homa Bay Town',
      'Ndhiwa',
      'Mbita',
      'Suba',
    ],
  },
  {
    name: 'Migori',
    code: '044',
    capital: 'Migori',
    sub_counties: [
      'Rongo',
      'Awendo',
      'Suna East',
      'Suna West',
      'Uriri',
      'Nyatike',
      'Kuria West',
      'Kuria East',
    ],
  },
  {
    name: 'Kisii',
    code: '045',
    capital: 'Kisii',
    sub_counties: [
      'Bonchari',
      'South Mugirango',
      'Bomachoge Borabu',
      'Bobasi',
      'Bomachoge Chache',
      'Nyaribari Chache',
      'Nyaribari Masaba',
      'Kitutu Chache North',
      'Kitutu Chache South',
    ],
  },
  {
    name: 'Nyamira',
    code: '046',
    capital: 'Nyamira',
    sub_counties: ['Kitutu Masaba', 'West Mugirango', 'North Mugirango', 'Borabu'],
  },
  {
    name: 'Nairobi',
    code: '047',
    capital: 'Nairobi',
    sub_counties: [
      'Westlands',
      'Dagoretti North',
      'Dagoretti South',
      'Langata',
      'Kibra',
      'Roysambu',
      'Kasarani',
      'Ruaraka',
      'Embakasi South',
      'Embakasi North',
      'Embakasi Central',
      'Embakasi East',
      'Embakasi West',
      'Makadara',
      'Kamukunji',
      'Starehe',
      'Mathare',
    ],
  },
]

const countyNames = ref([])
const countyFeatures = ref([])
const selectedCountyIndex = ref(0)
const selectedSubCountyIndex = ref(0)
const selectedCounty = ref(null)
let renderCountyFn = null

const selectCounty = (index) => {
  if (index === selectedCountyIndex.value) return
  selectedCountyIndex.value = index
  selectedSubCountyIndex.value = 0
  if (countyFeatures.value[index]) {
    selectedCounty.value = countyFeatures.value[index]
    if (renderCountyFn) {
      renderCountyFn(countyFeatures.value[index], selectedSubCountyIndex.value)
    }
  }
}

const selectSubCounty = (index) => {
  if (index === selectedSubCountyIndex.value) return
  selectedSubCountyIndex.value = index
  if (selectedCounty.value && renderCountyFn) {
    renderCountyFn(selectedCounty.value, index)
  }
}

onMounted(async () => {
  const width = 700
  const height = 600
  const svg = select('#mapSvg').attr('viewBox', `0 0 ${width} ${height}`)
  const tooltip = select('#tooltip')

  const geojson = await json(geojsonUrl)
  if (!geojson || !geojson.features) {
    console.error('Kenya GeoJSON not loaded', geojson)
    return
  }

  console.log('=== MAP DEBUG ===')
  console.log(`Raw GeoJSON features: ${geojson.features.length}`)
  console.log('Sample feature properties:', geojson.features[0]?.properties)

  // Use all features (no restrictive filter)
  const kenyaFeatures = geojson.features

  const countyGroups = groups(
    kenyaFeatures,
    (feature) => feature.properties?.adm1_name || feature.properties?.adm1_ref_name,
  )

  console.log(`County groups: ${countyGroups.length}`)
  countyGroups.forEach(([name, frags]) => {
    console.log(`  ${name}: ${frags.length} sub-counties`)
  })

  const mergeCountyGeometries = (fragments) =>
    fragments.flatMap((fragment) => {
      const geometry = fragment.geometry || {}
      if (geometry.type === 'Polygon') return [geometry.coordinates]
      if (geometry.type === 'MultiPolygon') return geometry.coordinates
      return []
    })

  countyFeatures.value = countyGroups
    .map(([name, fragments]) => {
      const normalizedName = name?.toString().trim() || 'Unknown'
      const extraInfo =
        richCountyData.find(
          (county) => county.name.toLowerCase() === normalizedName.toLowerCase(),
        ) || {}

      return {
        type: 'Feature',
        properties: {
          name: normalizedName,
          capital: extraInfo.capital || 'N/A',
          code: extraInfo.code || 'N/A',
          sub_counties: fragments.map(
            (fragment) =>
              fragment.properties?.adm2_name || fragment.properties?.adm2_ref_name || 'Unknown',
          ),
        },
        geometry: {
          type: 'MultiPolygon',
          coordinates: mergeCountyGeometries(fragments),
        },
        fragments,
      }
    })
    .sort((a, b) => a.properties.name.localeCompare(b.properties.name))

  const collectCoordinates = (geometry) => {
    if (!geometry || !geometry.type || !geometry.coordinates) return []
    const coords = []

    if (geometry.type === 'Polygon') {
      geometry.coordinates.forEach((ring) => ring.forEach((coordinate) => coords.push(coordinate)))
    } else if (geometry.type === 'MultiPolygon') {
      geometry.coordinates.forEach((polygon) =>
        polygon.forEach((ring) => ring.forEach((coordinate) => coords.push(coordinate))),
      )
    }

    return coords
  }

  const getGeoBounds = (features) => {
    const bounds = {
      minLon: 180,
      maxLon: -180,
      minLat: 90,
      maxLat: -90,
    }

    features.forEach((feature) => {
      collectCoordinates(feature.geometry).forEach(([lon, lat]) => {
        bounds.minLon = Math.min(bounds.minLon, lon)
        bounds.maxLon = Math.max(bounds.maxLon, lon)
        bounds.minLat = Math.min(bounds.minLat, lat)
        bounds.maxLat = Math.max(bounds.maxLat, lat)
      })
    })

    return bounds
  }

  const kenyaBounds = getGeoBounds(kenyaFeatures)
  console.log(
    `Kenya bounds: [[${kenyaBounds.minLon}, ${kenyaBounds.minLat}], [${kenyaBounds.maxLon}, ${kenyaBounds.maxLat}]]`,
  )
  const centerLon = (kenyaBounds.minLon + kenyaBounds.maxLon) / 2
  const centerLat = (kenyaBounds.minLat + kenyaBounds.maxLat) / 2

  const baseProjection = geoMercator().center([centerLon, centerLat]).scale(1).translate([0, 0])
  const projectedPoints = []
  kenyaFeatures.forEach((feature) => {
    collectCoordinates(feature.geometry).forEach(([lon, lat]) => {
      const [x, y] = baseProjection([lon, lat])
      if (Number.isFinite(x) && Number.isFinite(y)) {
        projectedPoints.push([x, y])
      }
    })
  })

  const xValues = projectedPoints.map(([x]) => x)
  const yValues = projectedPoints.map(([, y]) => y)
  const projectedMinX = Math.min(...xValues)
  const projectedMaxX = Math.max(...xValues)
  const projectedMinY = Math.min(...yValues)
  const projectedMaxY = Math.max(...yValues)
  const scale =
    Math.min(width / (projectedMaxX - projectedMinX), height / (projectedMaxY - projectedMinY)) *
    0.92
  const translateX = (width - scale * (projectedMinX + projectedMaxX)) / 2
  const translateY = (height - scale * (projectedMinY + projectedMaxY)) / 2

  const projection = geoMercator()
    .center([centerLon, centerLat])
    .scale(scale)
    .translate([translateX, translateY])
  const pathGenerator = geoPath().projection(projection)

  svg.append('rect').attr('width', width).attr('height', height).attr('fill', '#091014')

  // Debug: log each county's raw bounds using the helper
  countyFeatures.value.forEach((county) => {
    const bounds = getGeoBounds(county.fragments)
    console.log(
      `${county.properties.name}: bounds [[${bounds.minLon}, ${bounds.minLat}], [${bounds.maxLon}, ${bounds.maxLat}]]`,
    )
  })

  const drawSelectedCounty = (county, activeSubCountyIndex = selectedSubCountyIndex.value) => {
    if (!county) return
    svg.selectAll('g.county').remove()

    const countyGroup = svg.append('g').attr('class', 'county')

    countyGroup
      .selectAll('path')
      .data(county.fragments.map((fragment, i) => ({ ...fragment, fragmentIndex: i })))
      .enter()
      .append('path')
      .attr('d', (fragment) => pathGenerator(fragment))
      .attr('fill', 'none')
      .attr('stroke', (fragment) =>
        fragment.fragmentIndex === activeSubCountyIndex ? '#a6f3ff' : '#ffffff',
      )
      .attr('stroke-width', (fragment) =>
        fragment.fragmentIndex === activeSubCountyIndex ? 2.2 : 1.1,
      )
      .attr('stroke-linejoin', 'round')
      .attr('cursor', 'pointer')
      .on('mouseover', function (event) {
        select(this).attr('stroke', '#a6f3ff').attr('stroke-width', 1.8)
        tooltip
          .html(`<strong>${county.properties.code}</strong>`)
          .style('left', `${event.pageX + 15}px`)
          .style('top', `${event.pageY - 30}px`)
          .style('opacity', 1)
      })
      .on('mousemove', (event) => {
        tooltip.style('left', `${event.pageX + 15}px`).style('top', `${event.pageY - 30}px`)
      })
      .on('mouseout', function (event, fragment) {
        const isActive = fragment.fragmentIndex === activeSubCountyIndex
        select(this)
          .attr('stroke', isActive ? '#a6f3ff' : '#ffffff')
          .attr('stroke-width', isActive ? 2.2 : 1.1)
        tooltip.style('opacity', 0)
      })

    const pathCount = svg.selectAll('path').size()
    console.log(`Rendered fragment paths: ${pathCount}`)
  }

  countyNames.value = countyFeatures.value.map((county) => county.properties.name)
  if (countyFeatures.value.length > 0) {
    selectedCountyIndex.value = 0
    selectedSubCountyIndex.value = 0
    selectedCounty.value = countyFeatures.value[0]
    renderCountyFn = drawSelectedCounty
    drawSelectedCounty(countyFeatures.value[0], selectedSubCountyIndex.value)
  }

  console.log(`County groups appended: ${countyFeatures.value.length}`)
})
</script>
