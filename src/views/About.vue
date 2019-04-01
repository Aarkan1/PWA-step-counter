<template>
  <div class="about">
    <h1>This is an about page</h1>
    <br>
    <h3>Left/Right: {{leftRight}}</h3>
    <h3>Front/Back: {{frontBack}}</h3>
    <h3>Dir: {{dir}}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      leftRight: 0,
      frontBack: 0,
      dir: 0
    };
  },
  created() {
    if ("DeviceOrientationEvent" in window) {
      window.addEventListener(
        "deviceorientation",
        deviceOrientationHandler,
        false
      );
    } 

    function deviceOrientationHandler(eventData) {
      this.leftRight = eventData.gamma;
      this.frontBack = eventData.beta;
      this.dir = eventData.alpha;
    }

    // let gyroscope = new Gyroscope();
    // gyroscope.start();

    // gyroscope.onreading = e => {
    //   this.leftRight = gyroscope.x.toFixed(4);
    //   this.frontBack = gyroscope.y.toFixed(4);
    //   this.dir = gyroscope.z.toFixed(4);
    // };
    // gyroscope.onerror = e => {
    //   this.leftRight = "ERROR";
    // };
  }
};
</script>
