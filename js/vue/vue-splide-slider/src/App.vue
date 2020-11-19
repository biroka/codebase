<template>
  <div id="app">
    <h1>Howdy</h1>
    <Display />
    <BasicExample />
    <AutoplayExample />
    <ThumbnailExample />
    <DynamicSlideExample />
    <VideoExample />
  </div>
</template>

<script>
import "@splidejs/splide/dist/css/themes/splide-default.min.css";
import Display from "./components/Display";
import BasicExample from "./components/BasicExample";
import AutoplayExample from "./components/AutoplayExample";
import ThumbnailExample from "./components/ThumbnailsExample";
import DynamicSlideExample from "./components/DynamicSlidesExample";
import VideoExample from "./components/VideoExample";

export default {
  components: {
    Display,
    BasicExample,
    AutoplayExample,
    ThumbnailExample,
    DynamicSlideExample,
    VideoExample,
  },
};
</script>
