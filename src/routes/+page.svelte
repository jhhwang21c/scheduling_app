<script>
	import gcal_icon from '$lib/assests/gcal_icon.png';

	// isDragging, startColor, isPreferred variables came from ChatGPT
	let isDragging = false;
	let startColor = null; // green or yellow
	let currColor = null; // green, yellow, or white
	let isPreferred = false;
	let isSync = false;
	let syncText = 'Show';

	function getColor() {
		startColor = isPreferred ? 'green' : 'yellow';
	}

	// handleMouseDown, handleMouseMove, and handleMouseUp function ideas came from ChatGPT
	function handleMouseDown(event) {
		isDragging = true;
		const target = event.target;
		if (target.classList.contains('grid-item')) {
			currColor = target.style.backgroundColor;
			getColor(event);
			handleMouseMove(event);
		}
	}

	function handleMouseMove(event) {
		if (isDragging) {
			const target = event.target;
			if (target.classList.contains('grid-item')) {
				toggleCellColor(target);
			}
		}
	}

	function handleMouseUp() {
		isDragging = false;
	}

	function togglePreferredTime() {
		isPreferred = !isPreferred;
		getColor();
	}

	function toggleCellColor(cell) {
		if (startColor === 'green' && currColor == 'yellow' && cell.style.backgroundColor === '') { // do not allow users to change blank times to green
			cell.style.backgroundColor = '';
		} else {
			if (startColor === 'green' && currColor === 'yellow') { // can only select green times from set of yellow times
				cell.style.backgroundColor = 'green';
			}
			if (startColor === 'green' && currColor === 'green' && cell.style.backgroundColor !== '') { // when deselect green on green toggle, goes back to yellow
				cell.style.backgroundColor = 'yellow';
			}
			if (startColor === 'yellow' && currColor === '') { // first select yellow times
				cell.style.backgroundColor = 'yellow';
			}
			if (startColor === 'yellow' && currColor !== '') { // deselect yellow + green times when toggle is on yellow -> blank
				cell.style.backgroundColor = '';
			}
		}
	}

	function syncCal() {
		isSync = !isSync;
		if (isSync) {
			syncText = 'Hide'
		} else {
			syncText = 'Show'
		}
		document.querySelectorAll('.this').forEach(el => {
			el.classList.toggle('sync');
		});

		document.querySelectorAll('.conflict').forEach(el => {
			el.classList.toggle('hide');
		});
	}

</script>

<div class="sync"></div>
<div class="hide"></div>
<button on:click={syncCal} class="button"><img class="gcal" src={gcal_icon} width="20px" alt="gcal icon" />{syncText}
	Google
	Calendar</button>

<div class="togglebox">
	<span style="margin-right: 10px;">Available</span>
	<label class="switch">
		<input type="checkbox" bind:checked={isPreferred} on:click={togglePreferredTime}>
		<span class="slider round"></span>
	</label>
	<span style="margin-left: 10px;">Preferred</span>
</div>
<div class="instruction">
	<ol>
		<li><u>Show</u> or <u>hide</u> Google Calendar by pressing the button
			<ol style="list-style-type: lower-alpha; padding-bottom: 0;">
				<li style="margin-left:2em">Hover over Google Calendar events to display event name
				</li>
			</ol>
		</li>
		<br>
		<li><u>Toggle button on Available:</u> Select all available times (yellow)
		</li>
		<br>
		<li><u>Toggle button on Preferred:</u> From all available times (yellow), select preferred times (green)</li>
		<br>
		*Saved Immediately*
	</ol>

</div>
<div class="content">


	<div class="cal-container"><b class="month">February 2024</b>
		<div class="grid-container" role="grid" tabindex="-1" on:mousemove={handleMouseMove}
			on:mousedown={handleMouseDown} on:mouseup={handleMouseUp}>
			<div class="days">Mon 12</div>
			<div class="days">Tue 13</div>
			<div class="days">Wed 14</div>
			<div class="days">Thu 15</div>
			<div class="days">Fri 16</div>
			<div class="grid-item">9:00</div>
			<div class="grid-item">9:00</div>
			<div class="grid-item">9:00</div>
			<div class="grid-item">9:00</div>
			<div class="grid-item">9:00</div>

			<div class="grid-item">9:30</div>
			<div class="grid-item">9:30</div>
			<div class="grid-item">9:30</div>
			<div class="grid-item">9:30</div>
			<div class="grid-item">9:30</div>

			<div class="grid-item">10:00</div>
			<div class="grid-item">10:00</div>
			<div class="grid-item">10:00</div>
			<div class="grid-item">10:00</div>
			<div class="grid-item">10:00</div>

			<div class="grid-item">10:30</div>
			<div class="grid-item">10:30</div>
			<div class="grid-item">10:30</div>
			<div class="grid-item this">10:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA Section</span></div>
			</div>
			<div class="grid-item">10:30</div>

			<div class="grid-item">11:00</div>
			<div class="grid-item">11:00</div>
			<div class="grid-item">11:00</div>
			<div class="grid-item this">11:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA Section</span></div>
			</div>
			<div class="grid-item">11:00</div>

			<div class="grid-item">11:30</div>
			<div class="grid-item">11:30</div>
			<div class="grid-item">11:30</div>
			<div class="grid-item">11:30</div>
			<div class="grid-item">11:30</div>

			<div class="grid-item">12:00</div>
			<div class="grid-item this">12:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA 11</span></div>
			</div>
			<div class="grid-item">12:00</div>
			<div class="grid-item this">12:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA 11</span></div>
			</div>
			<div class="grid-item">12:00</div>

			<div class="grid-item">12:30</div>
			<div class="grid-item this">12:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA 11</span></div>
			</div>
			<div class="grid-item this">12:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">Lunch with Bob</span></div>
			</div>
			<div class="grid-item this">12:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA 11</span></div>
			</div>
			<div class="grid-item">12:30</div>

			<div class="grid-item">13:00</div>
			<div class="grid-item this">13:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA 11</span></div>
			</div>
			<div class="grid-item this">13:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">Lunch with Bob</span></div>
			</div>
			<div class="grid-item this">13:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">HAA 11</span></div>
			</div>
			<div class="grid-item">13:00</div>

			<div class="grid-item this">13:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">GENED 1046</span></div>
			</div>
			<div class="grid-item this">13:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">GENED Section</span></div>
			</div>
			<div class="grid-item this">13:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">GENED 1046</span></div>
			</div>
			<div class="grid-item">13:30</div>
			<div class="grid-item">13:30</div>

			<div class="grid-item this">14:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">GENED 1046</span></div>
			</div>
			<div class="grid-item this">14:00<div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">GENED Section</span></div>
			</div>
			<div class="grid-item this">14:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">GENED 1046</span></div>
			</div>
			<div class="grid-item">14:00</div>
			<div class="grid-item">14:00</div>

			<div class="grid-item">14:30</div>
			<div class="grid-item">14:30</div>
			<div class="grid-item">14:30</div>
			<div class="grid-item">14:30</div>
			<div class="grid-item">14:30</div>

			<div class="grid-item">15:00</div>
			<div class="grid-item">15:00</div>
			<div class="grid-item">15:00</div>
			<div class="grid-item">15:00</div>
			<div class="grid-item">15:00</div>

			<div class="grid-item this">15:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">CS 178</span></div>
			</div>
			<div class="grid-item">15:30 </div>
			<div class="grid-item this">15:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">CS 178</span></div>
			</div>
			<div class="grid-item">15:30</div>
			<div class="grid-item">15:30</div>

			<div class="grid-item this">16:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">CS 178</span></div>
			</div>
			<div class="grid-item ">16:00 </div>
			<div class="grid-item this">16:00 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">CS 178</span></div>
			</div>
			<div class="grid-item">16:00</div>
			<div class="grid-item">16:00</div>

			<div class="grid-item this">16:30<div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">CS 178</span></div>
			</div>
			<div class="grid-item ">16:30 </div>
			<div class="grid-item this">16:30 <div class="conflict tooltip" style="display: none;">...<span
						class="tooltiptext">CS 178</span></div>
			</div>
			<div class="grid-item ">16:30 </div>
			<div class="grid-item">16:30</div>
		</div>
	</div>

</div>

<style>
	.instruction {
		position: absolute;
		left: 5%;
		top: 200px;
		border: 1px solid black;
		border-radius: 20px;
		padding: 10px;
		width: 490px;
		font-size: 18px;
	}

	.content {
		position: absolute;
		width: 600px;
		right: 12%;
		padding-top: 40px;
	}

	.button {
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 14px;
		position: fixed;
		left: 100px;
		top: 100px
	}

	.togglebox {
		display: flex;
		justify-content: center;
		align-items: center;
		font-size: 14px;
		position: fixed;
		left: 350px;
		top: 95px;
	}

	.gcal {
		margin-right: 5px;
	}

	.hide {
		display: block !important;
	}

	.cal-container {
		background-color: #86c5f8;
		border-radius: 20px;
		padding: 10px 20px 20px 20px;
		width: 600px;
		text-align: center;
		margin-top: 20px;
	}

	.grid-container {
		display: grid;
		grid-template-columns: auto auto auto auto auto;
		margin-top: 10px;
	}

	.grid-item {
		background-color: rgba(255, 255, 255, 0.8);
		border: 1px solid rgba(0, 0, 0, 0.8);
		height: 20px;
		padding: 5px;
		font-size: 12px;
		text-align: center;
		user-select: none;
	}

	.month {
		font-size: 20px;
	}

	.days {
		text-align: center;
		font-weight: bold;
		font-size: 16px;
	}

	.sync {
		background-color: rgb(254, 155, 155);
	}

	/* Toggle button CSS, from https://www.w3schools.com/howto/howto_css_switch.asp */
	.switch {
		position: relative;
		display: inline-block;
		width: 60px;
		height: 34px;
		border: 1px solid black;
		border-radius: 70px;
	}

	.switch input {
		opacity: 0;
		width: 0;
		height: 0;
	}

	.slider {
		position: absolute;
		cursor: pointer;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: yellow;
		-webkit-transition: .4s;
		transition: .4s;
		border-color: black;
		border-radius: 100%;
	}

	.slider:before {
		position: absolute;
		content: "";
		height: 26px;
		width: 26px;
		left: 4px;
		bottom: 4px;
		background-color: rgb(230, 230, 230);
		-webkit-transition: .4s;
		transition: .4s;
		border-color: black;
	}

	input:checked+.slider {
		background-color: green;
	}

	input:focus+.slider {
		box-shadow: 0 0 1px green;
	}

	input:checked+.slider:before {
		-webkit-transform: translateX(26px);
		-ms-transform: translateX(26px);
		transform: translateX(26px);
	}

	/* Rounded sliders */
	.slider.round {
		border-radius: 34px;
		border-color: black;
	}

	.slider.round:before {
		border-radius: 50%;
		border-color: black;
	}


	.tooltip {
		position: relative;
		bottom: 15px;
		right: -80px;
		font-weight: bold;
		width: 30px;
	}

	.tooltip .tooltiptext {
		visibility: hidden;
		width: 100px;
		background-color: black;
		color: #fff;
		text-align: center;
		font-weight: lighter;
		border-radius: 6px;
		padding: 3px 0;
		position: absolute;
		z-index: 1;
	}

	.tooltip:hover .tooltiptext {
		visibility: visible;
	}
</style>