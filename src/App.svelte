<script type="module" lang="ts">
import Clock from "./lib/Clock.svelte";
import BackgroundGrid from "./lib/BackgroundGrid.svelte";
import {GLTFLoader} from "three/examples/jsm/loaders/GLTFLoader";
import * as Three from "three";
import {onMount} from "svelte";

let canvas:HTMLCanvasElement;
onMount(()=>{
    let scene = new Three.Scene();
    let renderer = new Three.WebGLRenderer({
        canvas: canvas!,
        antialias: true,
    });

    renderer.outputColorSpace = Three.SRGBColorSpace;
    let camera = new Three.PerspectiveCamera(30,1);
    camera.position.set(0,50,100);
    camera.lookAt(0,0,0);

    scene.background = new Three.Color(0xffffff);
    let light = new Three.DirectionalLight(0xffffff,3);
    light.position.set(0,50,100);
    scene.add(light);

    const loader = new GLTFLoader();
    loader.load("/chicken-model/scene.gltf",(model) => {
        scene.add(model.scene);
        let tick = 0;
        function animate() {
            requestAnimationFrame(animate);
            model.scene.rotation.y += Math.PI/100;
            renderer.render(scene,camera);
        }
        animate();
    });
});

</script>

<main>
    <Clock />
    <canvas bind:this={canvas} id="canvas" width="1920" height="1080"></canvas>
<!--    <BackgroundGrid/>-->
</main>

<style>
    main {
        height: 100%;
        width: 100%;
    }
    #canvas {
        display: block;
        width: 100vw;
        height: 100vh;
    }
</style>
