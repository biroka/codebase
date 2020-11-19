<template>
  <splide :options="options">
    <splide-slide>
      <img src="https://source.unsplash.com/random/800x450" />
    </splide-slide>
    <splide-slide>
      <img src="https://source.unsplash.com/random/800x450" />
    </splide-slide>
    <splide-slide>
      <img src="https://source.unsplash.com/random/800x450" />
    </splide-slide>
  </splide>
</template>

<script>
export default {
  data() {
    return {
      options: {
        rewind: true,
        width: 800,
        gap: "1rem",
      },
    };
  },
};
</script>