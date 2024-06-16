<script>
import HeaderComponent from '@/components/Header.vue';
import FooterComponent from '@/components/Footer.vue';
export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
    FooterComponent
  },
  data() {
    return {
      from: 'Ubicación actual',
      to: '',
      output: '',
      map: null,
      directionsService: null,
      directionsDisplay: null,
      currentLocation: { lat: null, lng: null },
      marker: null,
      autocomplete: null
    };
  },
  mounted() {
    this.loadGoogleMapsScript();
  },
  methods: {
    loadGoogleMapsScript() {
      const script = document.createElement('script');
      script.src = `https://maps.googleapis.com/maps/api/js?key=AIzaSyACm59KYQwLY8PFPEHZcBhlt-jRj8i6kV8&libraries=places`;
      script.async = true;
      script.defer = true;
      script.onload = this.initMap;
      document.head.appendChild(script);
    },
    initMap() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          this.currentLocation.lat = position.coords.latitude;
          this.currentLocation.lng = position.coords.longitude;
          this.from = `${this.currentLocation.lat}, ${this.currentLocation.lng}`;
          const mapOptions = {
            center: this.currentLocation,
            zoom: 15,
            mapTypeId: window.google.maps.MapTypeId.ROADMAP
          };

          this.map = new window.google.maps.Map(this.$refs.googleMap, mapOptions);
          this.directionsService = new window.google.maps.DirectionsService();
          this.directionsDisplay = new window.google.maps.DirectionsRenderer();
          this.directionsDisplay.setMap(this.map);

          // Marcar la ubicación actual
          this.marker = new window.google.maps.Marker({
            position: this.currentLocation,
            map: this.map,
            title: "Current Location"
          });
          //Para que la ubicación actual y sugerencias sea más exacta
          const bounds = new window.google.maps.LatLngBounds(
            new window.google.maps.LatLng(this.currentLocation.lat - 0.05, this.currentLocation.lng - 0.05),
            new window.google.maps.LatLng(this.currentLocation.lat + 0.05, this.currentLocation.lng + 0.05)
          );

          const options = {
            bounds: bounds,
            types: ['establishment'],
            location: new window.google.maps.LatLng(this.currentLocation.lat, this.currentLocation.lng),
            radius: 5000 // 5 km
          };
          const input2 = document.getElementById('to');
          this.autocomplete = new window.google.maps.places.Autocomplete(input2, options);

          this.autocomplete.addListener('place_changed', () => {
            const place = this.autocomplete.getPlace();
            if (!place.geometry) {
              console.error("Autocomplete's returned place contains no geometry");
              return;
            }

            this.to = place.formatted_address;
          });

        }, (error) => {
          console.error("Geolocation error:", error);
          this.handleLocationError(true);
        });
      } else {
        console.error("Browser doesn't support Geolocation");
        this.handleLocationError(false);
      }
    },
    handleLocationError(browserHasGeolocation) {
      const errorMessage = browserHasGeolocation ?
        'Error: The Geolocation service failed.' :
        'Error: Your browser doesn\'t support geolocation.';
      console.error(errorMessage);
      this.output = `<div class='alert-danger'><i class='fas fa-exclamation-triangle'></i> ${errorMessage}</div>`;
    },
    calcRoute() {
      const request = {
        origin: this.from,
        destination: this.to,
        travelMode: window.google.maps.TravelMode.DRIVING,
        unitSystem: window.google.maps.UnitSystem.IMPERIAL
      };

      this.directionsService.route(request, (result, status) => {
        if (status === window.google.maps.DirectionsStatus.OK) {
          this.output = `<div class='alert-info'>From: Current Location.<br />To: ${this.to}.<br /> Driving distance <i class='fas fa-road'></i> : ${result.routes[0].legs[0].distance.text}.<br />Duration <i class='fas fa-hourglass-start'></i> : ${result.routes[0].legs[0].duration.text}.</div>`;
          this.directionsDisplay.setDirections(result);
        } else {
          this.directionsDisplay.setDirections({ routes: [] });
          this.map.setCenter(this.currentLocation);
          this.output = "<div class='alert-danger'><i class='fas fa-exclamation-triangle'></i> Could not retrieve driving distance.</div>";
        }
      });
    }
  }
};
</script>

<template>
  <div id="home">
    <HeaderComponent />
    <div class="container">
      <div id="escoger-destino">
        <div class="container-main">
      <div class="container-fluid">
        <form class="form-horizontal">
          <div class="form-group">
            <label for="from" class="col-xs-2 control-label"><i class="far fa-dot-circle"></i></label>
            <div class="col-xs-4">
              <input type="text" id="from" placeholder="Origin" class="input" v-model="from" readonly>
            </div>
          </div>
          <div class="form-group">
            <label for="to" class="col-xs-2 control-label"><i class="fas fa-map-marker-alt"></i></label>
            <div class="col-xs-4">
              <input type="text" id="to" placeholder="Destino" class="input" v-model="to">
            </div>
          </div>
        </form>
        <div class="col-xs-offset-2 col-xs-10">
          <button class="btn btn-info btn-lg" @click="calcRoute"><i class="fas fa-map-signs"></i>Buscar Viaje</button>
        </div>
      </div>
      <div class="container-fluid">
        <div id="googleMap" ref="googleMap"></div>
        <div id="output" v-html="output"></div>
      </div>
    </div>
      </div>
    </div>
    <FooterComponent />
  </div>
</template>

<style scoped>
#escoger-destino {
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  
}
<style scoped>
  body {
    color: #5bc0de;
    font-family: "Poppins", sans-serif;
  }
  
  .fa-map-marker-alt,
  .fa-dot-circle {
    color: #5bc0de;
  }
  
  .container-main {
    background-color: transparent;
    margin: 0;
    padding: 10px;
  }


  .container-main h1,
  .container-main p {
    text-align: center;
  }
  
  /*map*/
  #googleMap {
    width: 80%;
    height: 400px;
    margin: 10px auto;
  }
  
  #output {
    text-align: center;
    font-size: 2em;
    margin: 20px auto;
  }
  
  #mode {
    color: black;
  }
  
  .btn-info {
  display: inline-block;
  font-weight: 600;
  color: white; 
  background-color: black;
  border: none; 
  padding: 15px 30px; 
  font-size: 18px; 
  line-height: 1.5;
  border-radius: 15px; 
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.btn-info:hover {
  background-color: #333; 
  transform: scale(1.05);
}

.container-main input.input {
  width: 400px;
  padding: 15px;
  font-size: 18px; 
  border: 3px solid #000000;
  border-radius: 4px;
  margin-bottom: 20px;
}
  </style>

