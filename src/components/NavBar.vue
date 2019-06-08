<template>
<div>
  <b-container>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand>Taskapp</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav type="light">
        <b-nav-item href="#">Mytasks</b-nav-item>
        <b-nav-item href="#">Calendar</b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-item-dropdown text="Lang" right>
        <b-dropdown-item href="#">EN</b-dropdown-item>
        <b-dropdown-item href="#">ES</b-dropdown-item>
        <b-dropdown-item href="#">RU</b-dropdown-item>
        <b-dropdown-item href="#">FA</b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-item-dropdown right>
        <!-- Using 'button-content' slot -->
        <template slot="button-content"><em>User</em></template>
        <b-dropdown-item href="#">Profile</b-dropdown-item>
        <b-dropdown-item href="#">Sign Out</b-dropdown-item>
        </b-nav-item-dropdown>
        <b-nav-form>
        <b-form-input size="md" class="mr-sm-6 " placeholder="Search"></b-form-input>
        <b-button size="md" type="submit">Search</b-button>
        </b-nav-form>
      </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </b-container>
</div>
</template>
