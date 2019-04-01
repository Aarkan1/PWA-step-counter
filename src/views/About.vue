<template>
  <div class="about">
    <h1>This is an about page</h1>
    <br>
    <h3>Gyroscope: {{gyro}}</h3>
    <h3>Avarage: {{avarageGyro}}</h3>
    <h3>Steps: {{steps}}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gyro: 0,
      steps: 0,
      avarageGyro: 0
    };
  },
  created() {
    let gyroscope = new Gyroscope();
    gyroscope.start();

    let avarage = [];

    gyroscope.onreading = e => {
      let oldGyro = 0;
      
      let x = gyroscope.x;
      let y = gyroscope.y;
      let z = gyroscope.z;

      this.gyro = Math.sqrt(x * x + y * y + z * z);

      if (this.gyro > 0.7 && this.gyro > oldGyro) {
        avarage.push(this.gyro);

        this.avarageGyro =
          avarage.reduce((total, num) => total + num) / avarage.length;
        this.steps++;

        oldGyro = this.gyro;
      }
    };
    gyroscope.onerror = e => {
      this.gyro = "ERROR";
    };
  }
};
</script>
