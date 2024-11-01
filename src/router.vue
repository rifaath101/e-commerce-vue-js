<script>
import { createRouter, createWebHistory } from "vue-router"
import LoginComponent from "./LoginComponent"
import RegisterComponent from "./RegisterComponent"
import ShopComponent from "./ShopComponent"

const routes = [
  { path: "/", redirect: "/shop" },
  { path: "/login", name: "Login", component: LoginComponent },
  { path: "/register", name: "Register", component: RegisterComponent },
  { path: "/shop", name: "Shop", component: ShopComponent },
]

const router = createRouter({
  history: createWebHistory(),
  routes,
})

export default router
</script>
