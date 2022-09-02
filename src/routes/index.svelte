<script>
  import { onMount } from "svelte";

  import { longpress } from "./action";
  import { LazyImage } from "svelte-lazy-image";
  import LOGO from "./logo-small.png";
  import SubLogo from "./sublogo.png";
  import { loadingController } from "@ionic/core";
  import Preview from "./preview.svelte";
  const imageModules = import.meta.glob("./images/*.jpg");
  let imgArray = [];
  let loaded = false;
  let show_preview = false;
  let PREVIEW_PATH;
  var showLoading = async () => {
    const loading = await loadingController.create({
      message: "Loading...",
      duration: 100,
      cssClass: "custom-loading",
    });

    loading.present();
  };

  function preview(path) {
    show_preview = true;
    PREVIEW_PATH = path;
  }

  function share(data) {
    navigator.share();
  }
  function load_images() {
    for (const modulePath in imageModules) {
      imgArray.push(modulePath);
    }
    console.log(imgArray.length);
    loaded = true;
  }
  let pressed;
  onMount(() => {
    load_images();
  });
  // code here
</script>

<ion-header translucent="true">
  <ion-toolbar>
    <ion-title>
      <img class="logo" src={LOGO} alt="MedExpo2022" />
    </ion-title>
  </ion-toolbar>
</ion-header>

<ion-content fullscreen="true" class="ion-padding">
  <div id="container">
    <img class="sublogo" src={SubLogo} alt="MedExpo2022" />
    <div class="subheader">
      <strong>MedTech Gallery Expo 2022</strong>
    </div>

    <div>
      <!-- promise is pending -->

      <!-- promise was fulfilled -->

      {#if loaded}
        <!-- content here -->
        <ion-row>
          {#each imgArray as image}
            <!-- content here asd-->

            <ion-col
              use:longpress
            on:longpress={(e) => (pressed = true)}
              on:click={() => {
                preview("src/routes/" + image);
              }}
              size={4}
            >
              <LazyImage
                src="src/routes/{image}"
                placeholder="INDQ Medtech Expo 2022"
                alt={image}
              />
            </ion-col>
          {/each}
        </ion-row>
        {#if show_preview}
          <div class="preview_box">
            <div
              on:click={() => {
                show_preview = false;
              }}
              style="background-color: black;"
            >
              close
            </div>
            <Preview img_src={PREVIEW_PATH} />
          </div>
          <!-- content here -->
        {:else}
          <!-- else content here -->
        {/if}
      {:else}
        <!-- else content here -->
        {showLoading()}
      {/if}
    </div>
  </div>
</ion-content>

<style>
  ion-title {
    text-align: center;
    padding: 10px;
  }

  .logo {
    max-height: 30px;
  }

  .sublogo {
    max-height: 230px;
    min-height: 170px;
    border-radius: 10px;
  }
  #container {
    text-align: center;
  }

  .subheader {
    background-color: rgb(34, 33, 33);
    padding: 12px;
    border-radius: 10px;
    font-size: 21px;
    margin: 10px;
  }
  .images {
    min-width: 200px;
    max-width: 200px;
  }
  .preview_box div {
    position: fixed;
    top: 7vh;
    padding: 10px;
    z-index: 2;
    left: 0;
  }
</style>
