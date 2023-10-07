<script setup lang="ts">
import { onMounted, ref } from 'vue'
import * as THREE from 'three'

const mount = ref(null)

onMounted(() => {
  const scene = new THREE.Scene()
  const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)

  const renderer = new THREE.WebGLRenderer()
  renderer.setSize(window.innerWidth, window.innerHeight)
  mount.value.appendChild(renderer.domElement)

  const geometry = new THREE.BoxGeometry()
  const material = new THREE.MeshBasicMaterial({ color: yellow })
  const cube = new THREE.Mesh(geometry, material)

  scene.add(cube)
  camera.position.z = 5

  const animate = function () {
    requestAnimationFrame(animate)
    cube.rotation.x += 0.01
    cube.rotation.y += 0.01
    renderer.render(scene, camera)
  }

  animate()
})
</script>

<template>
  <div ref="mount">
    />
  </div>
</template>
