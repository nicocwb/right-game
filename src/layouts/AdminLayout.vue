<template>
    <q-layout view="hHh lpR fFf">

        <q-header elevated class="bg-green text-white" height-hint="98">
            <q-toolbar>
                <q-toolbar-title>
                    <q-icon name="sports_soccer" /> JogoCerto - Admin
                </q-toolbar-title>
                <q-btn dense color="light-secondary" icon="logout" label="Logout" @click="this.logout()" />
            </q-toolbar>

            <q-tabs align="left">
                <q-route-tab to="/admin/quadras" label="Suas Quadras" />
                <q-route-tab to="/admin/requisicoes" label="Requisições" />
            </q-tabs>

        </q-header>

        <q-page-container>
            <router-view />
        </q-page-container>


        <q-footer elevated class="bg-green text-white">
            <q-toolbar>
                <q-toolbar-title class="text-center">
                    <q-icon name="sports_soccer" />
                </q-toolbar-title>
            </q-toolbar>
        </q-footer>
    </q-layout>
</template>
<script>

export default {
  name: 'AdminLayout',
  methods: {
      logout() {
          this.$router.push('/secure/admin')
      }
  }
}
</script>

<style>
.q-card {
  width: 360px;
}
</style>