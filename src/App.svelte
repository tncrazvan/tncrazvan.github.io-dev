<script>
	import SideMenuSubheader from './shared/component/wrapper/menu/SideMenuSubheader.svelte';
	import SideMenuDivider from './shared/component/wrapper/menu/SideMenuDivider.svelte';
	import MaterialIcon from './shared/component/misc/MaterialIcon.svelte';
	import SideMenuItem from './shared/component/wrapper/menu/SideMenuItem.svelte';
	import SideMenu from './shared/component/wrapper/menu/SideMenu.svelte';
	import Theme from './shared/component/theme/Theme.svelte';
	import HomePage from './component/page/HomePage.svelte';
	import { Router, Route } from "svelte-routing";

	import '../node_modules/materialize-css/dist/js/materialize.min.js';
	import './style/fonts/Roboto/Roboto.css';
	import './style/materialicons/materialicons.css';
	import './style/materialize/materialize.css';
	import './style/scrollbar/scrollbar.css';
	import './style/margin/margin.css';
	import './style/padding/padding.css';
	import './style/_main/_main.css';

	let url = window.location.pathname;
</script>
<SideMenu
	background="/images/landscape.jpg"
	image="/images/profile-pic.jpg"
	title="Razvan Tanase"
	subtitle="tangent.jotey@gmail.com"
>
	<SideMenuItem icon="import_contacts">
		Posts
	</SideMenuItem>
	<SideMenuItem icon="info_outline">
		About me
	</SideMenuItem>
	<SideMenuItem icon="layers">
		Stack
	</SideMenuItem>
	<SideMenuDivider />
	<SideMenuSubheader icon="class">
		Projects & Libraries
	</SideMenuSubheader>
	<SideMenuItem icon="code">
		CatPaw
	</SideMenuItem>
	<SideMenuItem icon="code">
		Arcano
	</SideMenuItem>
</SideMenu>
<Router url="{url}">
    <Route path="/" component="{HomePage}" />
    <Route path="/index.html" component="{HomePage}" />
</Router>
<Theme/>