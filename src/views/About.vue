<template>
  <div class="about">
    <h1>This is an about page</h1>
    <br>
    <h3>Gyroscope: {{Gyroscope}}</h3>
    <h3>Left/Right: {{leftRight}}</h3>
    <h3>Front/Back: {{frontBack}}</h3>
    <h3>Dir: {{dir}}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      Gyroscope: 0,
      leftRight: 0,
      frontBack: 0,
      dir: 0
    };
  },
  created() {
    let gyroscope = new Gyroscope();
    gyroscope.start();

    gyroscope.onreading = e => {
      let x = gyroscope.x;
      let y = gyroscope.y;
      let z = gyroscope.z;

      this.Gyroscope = Math.sqrt(x * x + y * y + z * z);

      this.leftRight = gyroscope.x.toFixed(4);
      this.frontBack = gyroscope.y.toFixed(4);
      this.dir = gyroscope.z.toFixed(4);
    };
    gyroscope.onerror = e => {
      this.leftRight = "ERROR";
    };
  }
};
</script>
