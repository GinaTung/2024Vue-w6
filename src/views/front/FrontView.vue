<template>
    這是前台
    <nav>
        <RouterLink to="/">Home</RouterLink> |
        <RouterLink to="/about">About</RouterLink> |
        <RouterLink to="/products">產品列表</RouterLink> |
        <RouterLink to="/cart">購物車</RouterLink> |
        <RouterLink to="/login">管理者登入</RouterLink> |
        <RouterLink to="/admin/products">後台 產品列表</RouterLink>
    </nav>
    <RouterView></RouterView>
</template>
