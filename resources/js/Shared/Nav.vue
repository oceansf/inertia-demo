<script setup>
import NavLink from './NavLink.vue';

</script>

<template>
    <nav>
      <ul class="flex space-x-4">
        <li><NavLink href="/" :active="$page.component === 'Home'">Home</NavLink></li>
        <li><NavLink href="/users" :active="$page.component === 'Users/Index'">Users</NavLink></li>
        <li><NavLink href="/settings" :active="$page.component === 'Settings'">Settings</NavLink></li>
         <li><NavLink href="/logout" method="post" as="button">
             Log Out
         </NavLink></li>
      </ul>
    </nav>
</template>
