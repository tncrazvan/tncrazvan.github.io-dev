<script>
	import style from '../../svelte-shared/scripts/style.js';
	let text = "#f1f1f1";
	let theme={
		main:{
			background: "#232128",
			color: text,
			strongColor: "#922a1a",
			horizontalLine:{
				color: "#2e2a38"
			},
			checkbox:{
				color: text,
				label: {
					color: text
				},
				checked: {
					color: "#42a5f5",
					label:{
						color: "#42a5f5"
					}
				}
			},
			datepicker:{
				color: text,
				background: "#a12128"
			},
			input:{
				color: "#dea047",
				label:{
					color: "#dea047",
					active: {
						color: "#42a5f5"
					}
				},
				active:{
					color: "#42a5f5"
				},
				valid:{
					color: "#ffffff"
				},
				invalid:{
					color: "#c62828 "
				},
			},
			button:{
				border:{
					radius: "4px"
				},
				background: "transparent",
				color: "#fff",
				waves: "rgba(33, 150, 243, 0.25)",
				hover:{
					background: "auto",
					color: "auto"
				},
				active:{
					background: "auto",
					color: "#42a5f5"
				}
			},
			anchor:{
				color: "#23a9f2",
				hover:{
					color: "#62c0f4"
				},
				active:{
					color: "#0077b7"
				}
			},
			sidenav:{
				divider: {
					background: "#858585"
				},
				button:{
					background: "transparent",
					color: "#fabd2f",
					waves: "rgba(0, 0, 0, 0.25)",
					hover:{
						background: "transparent"
					}
				},
				subheader: {
					color: "#858585"
				}
			},
			collection:{
				background: "#232128",
				border: {
					color: "#232128"
				}
			}
		}
	};
	export let variables = {};
	
	let vars = {
		"--main-background": theme.main.background,
		"--main-color": theme.main.color,
		"--main-strongColor": theme.main.strongColor,
		
		"--main-datepicker-color": theme.main.datepicker.color,
		"--main-datepicker-background": theme.main.datepicker.background,
		
		"--main-checkbox-color": theme.main.checkbox.color,
		"--main-checkbox-label-color": theme.main.checkbox.label.color,
		"--main-checkbox-checked-color": theme.main.checkbox.checked.color,
		"--main-checkbox-checked-label-color": theme.main.checkbox.checked.label.color,
		
		"--main-input-color": theme.main.input.color,
		"--main-input-active-color": theme.main.input.active.color,
		"--main-input-label-color": theme.main.input.label.color,
		"--main-input-label-active-color": theme.main.input.label.active.color,
		"--main-input-valid-color": theme.main.input.valid.color,
		"--main-input-invalid-color": theme.main.input.invalid.color,
		
		"--main-button-color": theme.main.button.color,
		"--main-button-background": theme.main.button.background,
		"--main-button-border-radius": theme.main.button.border.radius,
		"--main-button-waves": theme.main.button.waves,
		"--main-button-hover-background": theme.main.button.hover.background,
		"--main-button-hover-color": theme.main.button.hover.color,
		"--main-button-active-background": theme.main.button.active.background,
		"--main-button-active-color": theme.main.button.active.color,

		"--main-anchor-color": theme.main.anchor.color,
		"--main-anchor-hover-color": theme.main.anchor.hover.color,
		"--main-anchor-active-color": theme.main.anchor.active.color,
		
		"--main-sidenav-divider-background": theme.main.sidenav.divider.background,
		"--main-sidenav-subheader-color": theme.main.sidenav.subheader.color,
		"--main-sidenav-button-color": theme.main.sidenav.button.color,
		"--main-sidenav-button-background": theme.main.sidenav.button.background,
		"--main-sidenav-button-waves": theme.main.sidenav.button.waves,
		"--main-sidenav-button-hover-background": theme.main.sidenav.button.hover.background,
		
		"--main-collection-background": theme.main.collection.background,
		"--main-collection-border-color": theme.main.collection.border.color,

		"--main-horizontalLine-color": theme.main.horizontalLine.color,
	};

	for(let key in variables){
		vars[key] = variables[key];
	}

	//setting css variable
	$: css=style({
		":root":vars
	});
</script>
{@html css}

<style>
	/*GENERAL*/
	:global(html,body){
		background-color: var(--main-background) !important;
		color: var(--main-color) !important;
	}

	:global(a){
		position: relative;
		color: var(--main-anchor-color) !important;
	}

	:global(a:hover){
		color: var(--main-anchor-hover-color) !important;
	}

	:global(a:active){
		color: var(--main-anchor-active-color) !important;
	}

	:global(a:visited){
		color: var(--main-anchor-visited-color) !important;
	}

	/*BUTTON*/
	:global(.btn:active){
		background-color: var(--main-button-active-background);
	}
	:global(.btn:hover){
		background-color: var(--main-button-hover-background);
	}
	:global(.btn){
		color: var(--main-button-color);
	}
	
	:global(.btn:not(.border-radius-0)){
		border-radius: var(--main-button-border-radius)
	}

	:global(.waves-effect .waves-ripple){
		/* The alpha value allows the text and background color
		of the button to still show through. */
		background-color: var(--main-button-waves);
	}

	/*BUTTON ON SIDENAV*/
	:global(.sidenav li:hover){
		background-color: var(--main-sidenav-button-background);
	}
	:global(.sidenav li){
		font-weight: 500;
		color: var(--main-sidenav-button-color);
	}
	
	:global(.sidenav li:not(.border-radius-0)){
		border-radius: 4px;
	}

	:global(.sidenav li.waves-effect .waves-ripple){
		/* The alpha value allows the text and background color
		of the button to still show through. */
		background-color: var(--main-sidenav-button-waves);
	}


	/*INPUT FIELD*/
	:global(.input-field label){
		color: var(--main-input-label-color) !important;
	}

	:global(.input-field label.active){
		color: var(--main-input-label-active-color) !important;
	}

	:global(.input-field input){
		color: var(--main-input-color) !important;
		border-color: var(--main-input-color) !important;
		box-shadow: 0 1px 0 0 var(--main-input-color) !important;
	}

	:global(.input-field input:focus){
		color: var(--main-input-active-color) !important;
		border-color: var(--main-input-active-color) !important;
		box-shadow: 0 1px 0 0 var(--main-input-active-color) !important;
	}

	:global(.input-field input.valid:not(:focus)){
		color: var(--main-input-valid-color) !important;
		border-color: var(--main-input-valid-color) !important;
		box-shadow: 0 1px 0 0 var(--main-input-valid-color) !important;
	}

	:global(.input-field input.invalid){
		color: var(--main-input-invalid-color) !important;
		border-color: var(--main-input-invalid-color) !important;
		box-shadow: 0 1px 0 0 var(--main-input-invalid-color) !important;
	}

	/*DATEPICKER*/
	:global(.modal.datepicker-modal.open){
		border-radius: 0.3rem;
		background: transparent;
	}
	:global(.datepicker-date-display){
		background-color: var(--main-datepicker-background) !important;
		color: var(--main-datepicker-color) !important;
	}
	:global(.datepicker-table td.is-selected){
		background-color: var(--main-datepicker-background) !important;
		color: var(--main-datepicker-color) !important;
	}
	:global(.datepicker-day-button:focus){
		opacity: 0.5;
		background-color: var(--main-datepicker-background) !important;
		color: var(--main-datepicker-color) !important;
	}
	:global(.datepicker-cancel,.datepicker-done){
		background-color: var(--main-button-background) !important;
		color: var(--main-button-color) !important;
	}
	:global(.datepicker-container .waves-effect .waves-ripple,.datepicker-container .waves-effect .waves-ripple){
		background-color: var(--main-button-waves) !important;
	}
	:global(.month-next svg,.month-prev svg){
		fill: var(--main-color) !important;
	}
	:global(.month-next:focus,.month-prev:focus){
		outline: none !important;
		background-color: var(--main-button-background) !important;
		color: var(--main-button-color) !important;
	}
	:global(.datepicker-calendar-container){
		background: var(--main-background) !important;
		color: var(--main-color) !important;
	}
	:global(.select-wrapper.select-month input,.select-wrapper.select-year input){
		color: var(--main-color) !important;
	}
	:global(.datepicker-table-wrapper th abbr){
		color: var(--main-color) !important;
	}
	:global(.datepicker-row .is-today){
		color: var(--main-anchor-color) !important;
	}

	/*DROPDOWN*/
	:global(.dropdown-content.select-dropdown){
		background-color: var(--main-background) !important;
	}
	:global(.dropdown-content li > a, .dropdown-content li > span){
		color: var(--main-anchor-color) !important;
	}

	/*SIDENAV*/
	:global(.sidenav){
		background-color: var(--main-background) !important;
	}
	:global(.sidenav .divider){
		background-color: var(--main-sidenav-divider-background) !important;
	}
	:global(.sidenav .subheader){
		color: var(--main-sidenav-subheader-color) !important;
	}
	
	/*COLLECTION*/
	:global(html, body, .collection, .collection-item, .collection .collection-item){
		background: var(--main-collection-background);
		color: var(--main-color);
		border-color: var(--main-horizontalLine-color);
	}

	/*HORIZONTAL LINE*/
	:global(hr){
		border: 0;
		height: 1px;
		width: 100%;
		background: var(--main-horizontalLine-color)
	}

	
</style>