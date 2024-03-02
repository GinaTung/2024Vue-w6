<template>
    <div class="container  my-5">
        <h2 class="text-center fw-bold mb-3">前台</h2>
    <nav class="text-center">
            <RouterLink to="/">Home</RouterLink> |
            <RouterLink to="/about">About</RouterLink> |
            <RouterLink to="/products">產品列表</RouterLink> |
            <RouterLink to="/cart">購物車</RouterLink> |
            <RouterLink to="/login">管理者登入</RouterLink> |
            <RouterLink to="/admin/products">後台產品列表</RouterLink>
        </nav>
        <RouterView></RouterView>
    </div>
</template>
