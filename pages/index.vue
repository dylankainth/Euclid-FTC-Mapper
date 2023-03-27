<template>
  <div>
    <center><h1>Team Euclid FTC Team Mapper</h1></center>

    <div id="map-wrap" style="height: 80vh">
      <client-only>
        <l-map :zoom="2" :center="[0, 0]">
          <l-tile-layer
            url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"
          ></l-tile-layer>

          <div v-for="pin in pins" :key="pin.id">
            <l-marker :lat-lng="[pin.team_location.lat, pin.team_location.lng]">
              <l-popup>
                <div>
                  Team
                  <a
                    :href="
                      'https://ftc-events.firstinspires.org/team/' +
                      pin.team_number_yearly
                    "
                    target="_blank"
                  >
                    <b>{{ pin.team_number_yearly }}</b>
                  </a>
                </div>
              </l-popup>
            </l-marker>
          </div>
        </l-map>
      </client-only>
    </div>

    <div class="container">
    <p class="px-5 pt-2" >Here's a quick mockup for the basic features of this website. It is not styled, so it doesn't yet look pretty or brand-consistent. Making a CSS Stylesheet to improve the look and feel of the website is next. This will include colours, images and user interface design</p>
  
    <p class="px-5">Also, teams at null island have dodgy data, so that needs to be fixed too.</p>

    <p class="px-5"><a href="https://dylankainth.com">~ Dylan</a></p>
  </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const pins = await $axios.$get('getMapPins')
    return { pins }
  },
}
</script>
