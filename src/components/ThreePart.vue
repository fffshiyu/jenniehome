<template>
  <div>
    <div id="scene-container"></div>
    <!-- Down arrow icon in the middle of the page -->
    <div class="arrow-container">
      <img class="arrow-down" src="../assets/images/arrow-down-filling.svg" alt="Arrow Down">
    </div>
     <!-- Text content above the square -->
     <div class="text-content">
      <p>你好，我是方是玉，欢迎来到我的主页，我是一名3D开发工程师，我在中国上海</p>
      <p>Hello, I'm Jennie Fofo. Welcome to my page! I am a 3D creative developer based in Shanghai, China.</p>
    </div>
  </div>
</template>
  
<script>
import * as THREE from 'three';
export default {
  name: 'ThreePart',
  mounted() {
    const container = document.getElementById('scene-container');
    const scene = new THREE.Scene();

    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.z = 5;

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    container.appendChild(renderer.domElement);

    const edgeMaterial = new THREE.MeshBasicMaterial({ color: 0x000000, wireframe: true });

    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const material = new THREE.MeshBasicMaterial({ color: 0xf4a7ba });

    const cube = new THREE.Mesh(geometry, material);
    cube.position.y +=1

    const cubeWithEdges = new THREE.Mesh(geometry, edgeMaterial);
 

    scene.add(cube);
    scene.add(cubeWithEdges);

    cubeWithEdges.position.copy(cube.position);

    const arrowContainer = document.querySelector('.arrow-container');
    arrowContainer.style.position = 'absolute';
    arrowContainer.style.bottom = '20px'; // Adjust the distance from the bottom as needed
    arrowContainer.style.left = '50%';
    arrowContainer.style.transform = 'translateX(-50%)'; // Center horizontally


    const animate = () => {
      requestAnimationFrame(animate);
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
      cubeWithEdges.rotation.x += 0.01;
      cubeWithEdges.rotation.y += 0.01;
      renderer.render(scene, camera);
    };

    animate();

    window.addEventListener('resize', () => {
      const newWidth = window.innerWidth;
      const newHeight = window.innerHeight;
      camera.aspect = newWidth / newHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(newWidth, newHeight);
    });
  },
};
</script>
  
<style scoped>
 .arrow-down {
  width: 30px; /* Adjust the width and height as needed */
  height: 30px;
}

.arrow-container {
  position: absolute;
  bottom: 20px; /* Adjust the distance from the bottom as needed */
  left: 50%;
  transform: translateX(-50%); /* Center horizontally */
}

.text-content {
  position: absolute;
  top: 20%; /* 根据需要调整距离顶部的距离 */
  left: 50%;
  transform: translateX(-50%); /* 水平居中 */
  text-align: center;
  color: #f4a7ba; /* 根据需要设置文本颜色 */
}
</style>
  