<template>
  <div>
    <canvas class="webgl"></canvas>
  </div>
</template>
  
<script>
// import './style.css'
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import * as dat from 'lil-gui'
// import typefaceFont from 'three/examples/fonts/helvetiker_regular.typeface.json'
import { FontLoader } from 'three/examples/jsm/loaders/FontLoader.js'
import { TextGeometry } from 'three/examples/jsm/geometries/TextGeometry.js'



export default {
  name: 'DonatPart',
  mounted() {
    /**
     * Base
     */
    // Debug
    const gui = new dat.GUI({ touchStyles: false })
    const params = {
      color: 0xf57120,
      size: 0.5
    }
    gui.hide()

    // Canvas
    const canvas = document.querySelector('canvas.webgl')

    // Scene
    const scene = new THREE.Scene()
    scene.background = new THREE.Color(0xf4a7ba);
    scene.fog = new THREE.Fog(0xf4a7ba, 1, 11)



    gui
      .addColor(params, 'color')
      .onChange(() => {
        scene.background.set(params.color)
      })
      .name('Background color')

    //Axes helper
    // const axesHelper = new THREE.AxesHelper()
    // scene.add(axesHelper)

    /**
* Textures
*/
    const textureLoader = new THREE.TextureLoader()
    const matcapTexture = textureLoader.load('http://localhost:8084/textures/matcaps/20.png')
    const matcapTexture2 = textureLoader.load('http://localhost:8084/textures/matcaps/3.png')

    const fontLoader = new FontLoader()


    fontLoader.load('http://localhost:8084/fonts/grotesk.typeface.json', (font) => {
      const textGeometry = new TextGeometry('JENNIE.FO', {
        font: font,
        size: params.size,
        height: 0.2,
        curveSegments: 5,
        bevelEnabled: true,
        bevelThickness: 0.03,
        bevelSize: 0.02,
        bevelOffset: 0,
        bevelSegments: 4
      })

      textGeometry.computeBoundingBox()
      textGeometry.center()

      const textMaterial = new THREE.MeshMatcapMaterial({ matcap: matcapTexture })
      const text = new THREE.Mesh(textGeometry, textMaterial)
      scene.add(text)

      const donutGeometry = new THREE.TorusGeometry(0.3, 0.2, 20, 45)
      const donutMaterial = new THREE.MeshMatcapMaterial({ matcap: matcapTexture2 })

      for (let i = 0; i < 200; i++) {
        const donut = new THREE.Mesh(donutGeometry, donutMaterial)
        scene.add(donut)

        donut.position.x = (Math.random() - 0.5) * 10
        donut.position.y = (Math.random() - 0.5) * 10
        donut.position.z = (Math.random() - 0.5) * 10

        donut.rotation.x = Math.random() * Math.PI
        donut.rotation.y = Math.random() * Math.PI

        const scale = Math.random()
        donut.scale.set(scale, scale, scale)
      }
    })

    /**
     * Sizes
     */
    const sizes = {
      width: window.innerWidth,
      height: window.innerHeight
    }

    window.addEventListener('resize', () => {
      // Update sizes
      sizes.width = window.innerWidth
      sizes.height = window.innerHeight

      // Update camera
      camera.aspect = sizes.width / sizes.height
      camera.updateProjectionMatrix()

      // Update renderer
      renderer.setSize(sizes.width, sizes.height)
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
    })

    /**
     * Camera
     */
    // Base camera
    const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height, 0.1, 100)
    camera.position.x = 1
    camera.position.y = 1
    camera.position.z = 2
    scene.add(camera)

    // Controls
    const controls = new OrbitControls(camera, canvas)
    controls.enableDamping = false
    controls.autoRotate =true
    controls.autoRotateSpeedm=0.01

    /**
     * Renderer
     */
    const renderer = new THREE.WebGLRenderer({
      canvas: canvas
    })
    renderer.setSize(sizes.width, sizes.height)
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))

    /**
     * Animate
     */
    const clock = new THREE.Clock()

    const tick = () => {
      // eslint-disable-next-line
      const elapsedTime = clock.getElapsedTime()

      // Update controls
      controls.update()

      // Render
      renderer.render(scene, camera)

      // Call tick again on the next frame
      window.requestAnimationFrame(tick)
    }

    tick()
  }
}

</script>
  
<style scoped>
/* 这里可以编写组件的样式 */
.webgl {
  width: 90%;
  z-index: 1;
  outline: none;
}
.canvas-container {
  overflow-x: hidden;
}

</style>
  