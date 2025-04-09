<template>
  <b-collapse class="sidebar-collapse" id="sidebar-collapse" :visible="sidebarOpened">
  <nav
    :class="{sidebar: true}"
  >
    <header class="logo">
      <router-link to="/app">Aloc <span class="fw-bold">AI</span></router-link>
    </header>

    <!-- <a class="generator-link navTitle" target="_blank" href="https://flatlogic.com/generator">Generate App</a> -->

    <ul class="nav">
      <NavLink
        :activeItem="activeItem"
        header="Dashboard"
        link="/app/dashboard"
        iconName="flaticon-home-3"
        index="dashboard"
        isHeader
      />
      <NavLink
        header="Typography"
        link="/app/typography"
        iconName="flaticon-list-3"
        index="typography"
        isHeader
      />
      <NavLink
        header="Tables Basic"
        link="/app/tables"
        iconName="flaticon-equal-3"
        index="tables"
        isHeader
      />
      <NavLink
        header="Notifications"
        link="/app/notifications"
        iconName="flaticon-bell"
        index="notifications"
        isHeader
      />
      <NavLink
        :activeItem="activeItem"
        header="Components"
        link="/app/components"
        iconName="flaticon-network-1"
        index="components"
        :childrenLinks="[
          { header: 'Charts', link: '/app/components/charts' },
          { header: 'Icons', link: '/app/components/icons' },
          { header: 'Maps', link: '/app/components/maps' },
        ]"
      />
    </ul>
    <h5 class="navTitle d-sm-down-none">
      LABELS
    </h5>
    <ul class="sidebarLabels d-sm-down-none">
      <li>
        <a href="#">
          <i class="fa fa-circle text-success mr-3" />
          <span class="labelName">Core</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="fa fa-circle text-primary mr-3" />
          <span class="labelName">UI Elements</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="fa fa-circle text-danger mr-3" />
          <span class="labelName">Forms</span>
        </a>
      </li>
    </ul>

    
  </nav>
  </b-collapse>
</template>

<script>
import { mapState, mapActions } from 'vuex';
import NavLink from './NavLink/NavLink';

export default {
  name: 'Sidebar',
  components: { NavLink },
  data() {
    return {
      alerts: [
        {
          id: 0,
          title: 'Sales Report',
          value: 15,
          footer: 'Calculating x-axis bias... 65%',
          color: 'primary',
        },
        {
          id: 1,
          title: 'Personal Responsibility',
          value: 20,
          footer: 'Provide required notes',
          color: 'danger',
        },
      ],
    };
  },
  methods: {
    ...mapActions('layout', ['changeSidebarActive', 'switchSidebar']),
    setActiveByRoute() {
      const paths = this.$route.fullPath.split('/');
      paths.pop();
      this.changeSidebarActive(paths.join('/'));
    },
  },
  created() {
    this.setActiveByRoute();
  },
  computed: {
    ...mapState('layout', {
      sidebarOpened: state => !state.sidebarClose,
      activeItem: state => state.sidebarActiveElement,
    }),
  },
};
</script>

<!-- Sidebar styles should be scoped -->
<style src="./Sidebar.scss" lang="scss" scoped/>
