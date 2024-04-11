<script type="module" lang="ts">
import Clock from "./lib/Clock.svelte";
import {type GLTF, GLTFLoader} from "three/examples/jsm/loaders/GLTFLoader";
import * as Three from "three";
import {onMount} from "svelte";

function addChicken(positionZ:number,scene:Three.Scene,renderer:Three.WebGLRenderer, camera:Three.PerspectiveCamera) {
    const loader = new GLTFLoader();
    loader.load("/chicken-model/scene.gltf",(model) => {
        scene.add(model.scene);
        model.scene.position.z = positionZ;
        model.scene.rotation.y = positionZ/260*2*Math.PI;
        let tick = (positionZ+200)/260*60;
        function animate() {
            requestAnimationFrame(animate);

            // model.scene.rotation.x += Math.PI/70;
            model.scene.rotation.y += Math.PI/50;
            model.scene.position.z += 0.7;
            // model.scene.position.x += Math.sin(Math.PI/30*tick++)/2;
            if(tick >= 60) tick = 0;
            if(model.scene.position.z > 60) {
                model.scene.position.z = -200;
            }
            renderer.render(scene,camera);
        }
        animate();
    });
}

function loadModel(modelPath:sting) {
    return new Promise<GLTF>((resolve,reject) => {
        const loader = new GLTFLoader();
        loader.load(modelPath,model => resolve(model),null,reject);
    });
}

let canvas:HTMLCanvasElement;
onMount(async ()=>{
    let scene = new Three.Scene();
    let renderer = new Three.WebGLRenderer({
        canvas: canvas!,
        antialias: true,
    });

    renderer.outputColorSpace = Three.SRGBColorSpace;
    let camera = new Three.PerspectiveCamera(30,1);
    camera.position.set(0,50,100);
    camera.lookAt(0,0,0);

    // const material = new Three.MeshBasicMaterial();
    // material.color = new Three.Color(0xff55aa);
    // const geometry = new Three.BoxGeometry(200,1,200);
    // const cube = new Three.Mesh(geometry,material);
    // cube.position.set(0,-10,0);
    // scene.add(cube);

    scene.background = new Three.Color(0xff55aa);
    let light = new Three.DirectionalLight(0xffffff,3);
    light.position.set(0,50,100);
    scene.add(light);

    // -200 ~ 60
    // for(let i = -200; i < 60; i+=positionGap) {
    //     addChicken(i,scene,renderer,camera);
    // }
    const positionGap = 260/4;
    let chickens:GLTF[] = [];
    for(let i = -200; i < 60; i+=positionGap) {
        chickens.push(await loadModel("/chicken-model/scene.gltf"));
    }
    chickens.forEach((chicken,i) => {
        const positionZ = i*positionGap - 200;
        chicken.scene.position.z = positionZ;
        chicken.scene.rotation.y = positionZ/260*2*Math.PI;
        scene.add(chicken.scene);
        function animate() {
            requestAnimationFrame(animate);
            chicken.scene.rotation.y += Math.PI/50;
            chicken.scene.position.z += 0.7;
            if(chicken.scene.position.z > 60) {
                chicken.scene.position.z = -200;
            }
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
        background-color: #ff55aa;
    }
    #canvas {
        display: block;
        width: 100%;
        height: 100%;
    }
</style>
