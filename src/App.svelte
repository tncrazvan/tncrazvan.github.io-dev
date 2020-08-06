<script>
import GridStyles from './svelte-shared/components/styles/GridStyles.svelte';
import PaddingStyles from './svelte-shared/components/styles/PaddingStyles.svelte';
import MarginStyles from './svelte-shared/components/styles/MarginStyles.svelte';
import Theme from './component/theme/Theme.svelte';
import HomePage from './component/page/HomePage.svelte';
import { Router, Route } from "svelte-routing";

import '../node_modules/materialize-css/dist/js/materialize.min.js';
import './style/fonts/Roboto/Roboto.css';
import './style/materialicons/materialicons.css';
import './style/materialize/materialize.css';
//import './style/scrollbar/scrollbar.css';
import './style/margin/margin.css';
import './style/padding/padding.css';
import './style/_main/_main.css';
import OtherStyles from './svelte-shared/components/styles/OtherStyles.svelte';

let url = window.location.pathname;
</script>
<Router url="{url}">
    <Route path="/" component="{HomePage}" />
    <Route path="/index.html" component="{HomePage}" />
</Router>
<GridStyles />
<OtherStyles />
<PaddingStyles />
<MarginStyles />
<Theme variables={{
	"--main-button-border-radius": "3rem",
	"--main-button-waves": "#922a1a"
}}/>

<style>

	:global(html,body){
		width: 100%;
		height: 100%;
		overflow-y: auto;
	}
	:global(th,td){
		padding: 1rem;
    	border-right: 1px solid var(--main-horizontalLine-color);
	}
	:global(th){
		background: rgba(0,0,0,0.25);
	}
	:global(table){
		background: var(--main-collection-background);
		border: 1px solid var(--main-horizontalLine-color);
	}
	:global(tr){
		border-color: var(--main-horizontalLine-color);
	}
</style>