<template>
  <div class="px-5 py-2 text-center list-item w-100 fs-5">
    <i class="bi bi-person-circle me-4"></i>
    <span>UserName</span>
  </div>
</template>

<style scoped>
.list-item {
  transition: all 0.225s ease-in-out;
}
.list-item:hover {
  transform: scale(1.05);
  cursor: pointer;
  color: #0d6efd;
  font-weight: bold;
}
</style>
