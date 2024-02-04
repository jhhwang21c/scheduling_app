<script>
	import gcal_icon from '$lib/assests/gcal_icon.png';

	let isDragging = false;
	let startColor = null; // green or yellow
	let currColor = null; // green, yellow, or white


	function getColor(event) {
		if (document.getElementById('preferred_time').checked) {
			startColor = 'green';
		}
		else {
			startColor = 'yellow';
		}
	}

	function handleMouseDown(event) {
		isDragging = true;
		const target = event.target;
		if (target.classList.contains('grid-item')) {
			// startColor = target.style.backgroundColor;
			currColor = target.style.backgroundColor;
			getColor(event);
			handleMouseMove(event);
		}
	}

	function handleMouseMove(event) {
		if (isDragging) {
			const target = event.target;
			// if (target.classList.contains('grid-item')) {
			// 	if (startColor === 'green') {
			// 		toggleCellColor(target);
			// 	} else {
			// 		if (target.style.backgroundColor !== 'green') {
			// 			toggleCellColor(target);
			// 		}
			// 	}
			// }
			if (target.classList.contains('grid-item')) {
				toggleCellColor(target);
			}
		}
	}

	function handleMouseUp() {
		isDragging = false;
	}

	function toggleCellColor(cell) {
		// cell.classList.toggle('highlight');

		// console.log('currColor: ' + currColor)
		// console.log('startColor: ' + startColor)
		// console.log(' ')
		if (startColor === 'green' && currColor == 'yellow' && cell.style.backgroundColor === '') { // do not allow users to change blank times to green
			cell.style.backgroundColor = '';
		} else {
			if (startColor === 'green' && currColor === 'yellow') { // can only select green times from set of yellow times
			cell.style.backgroundColor = 'green'; 
			}
			if (startColor === 'green' && currColor === 'green' && cell.style.backgroundColor !== '') { // when deselect green, goes back to yellow
				cell.style.backgroundColor = 'yellow'; 
			}
			if (startColor === 'yellow' && currColor === '') { // first select yellow times
				cell.style.backgroundColor = 'yellow'; 
			}
			if (startColor === 'yellow' && currColor !== '') { // deselect yellow times
				cell.style.backgroundColor = ''; 
			}
		}
	}

	function syncCal() {
		// var element = document.getElementById("1");
		// console.log(element);
		// element.classList.toggle("test");
		// classList.toggle("test");

		document.querySelectorAll('.this').forEach(el => {
			el.classList.toggle('test');
			console.log(el)
		});


	}

</script>

<button on:click={syncCal}><img src={gcal_icon} width="20px" alt="gcal icon" />sync with Google Calendar</button>
<div class="test"></div>

<input type="radio" id="not_preferred_time" name="time" value="not_preferred_time" checked />
<label for="not_preferred_time">Available, but Not Preferred</label>

<input type="radio" id="preferred_time" name="time" value="preferred_time" />
<label for="preferred_time">Preferred Time</label>

<div class="grid-container" role="grid" tabindex="-1" on:mousemove={handleMouseMove} on:mousedown={handleMouseDown}
	on:mouseup={handleMouseUp}>
	<div class="days">Mon</div>
	<div class="days">Tue</div>
	<div class="days">Wed</div>
	<div class="days">Thu</div>
	<div class="days">Fri</div>
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
	<div class="grid-item this">10:30</div>
	<div class="grid-item">10:30</div>

	<div class="grid-item">11:00</div>
	<div class="grid-item">11:00</div>
	<div class="grid-item">11:00</div>
	<div class="grid-item this">11:00</div>
	<div class="grid-item">11:00</div>

	<div class="grid-item">11:30</div>
	<div class="grid-item">11:30</div>
	<div class="grid-item">11:30</div>
	<div class="grid-item">11:30</div>
	<div class="grid-item">11:30</div>

	<div class="grid-item">12:00</div>
	<div class="grid-item this">12:00</div>
	<div class="grid-item">12:00</div>
	<div class="grid-item this">12:00</div>
	<div class="grid-item">12:00</div>

	<div class="grid-item">12:30</div>
	<div class="grid-item this">12:30</div>
	<div class="grid-item this">12:30</div>
	<div class="grid-item this">12:30</div>
	<div class="grid-item">12:30</div>

	<div class="grid-item">13:00</div>
	<div class="grid-item this">13:00</div>
	<div class="grid-item this">13:00</div>
	<div class="grid-item this">13:00</div>
	<div class="grid-item">13:00</div>

	<div class="grid-item this">13:30</div>
	<div class="grid-item this">13:30</div>
	<div class="grid-item this">13:30</div>
	<div class="grid-item">13:30</div>
	<div class="grid-item">13:30</div>

	<div class="grid-item this">14:00</div>
	<div class="grid-item this">14:00</div>
	<div class="grid-item this">14:00</div>
	<div class="grid-item">14:00</div>
	<div class="grid-item">14:00</div>

	<div class="grid-item">14:30</div>
	<div class="grid-item">14:30</div>
	<div class="grid-item">14:30</div>
	<div class="grid-item">14:30</div>
	<div class="grid-item">14:30</div>

	<div class="grid-item">15:00</div>
	<div class="grid-item this">15:00</div>
	<div class="grid-item">15:00</div>
	<div class="grid-item">15:00</div>
	<div class="grid-item">15:00</div>

	<div class="grid-item this">15:30</div>
	<div class="grid-item this">15:30</div>
	<div class="grid-item this">15:30</div>
	<div class="grid-item">15:30</div>
	<div class="grid-item">15:30</div>

	<div class="grid-item this">16:00</div>
	<div class="grid-item this">16:00</div>
	<div class="grid-item this">16:00</div>
	<div class="grid-item">16:00</div>
	<div class="grid-item">16:00</div>

	<div class="grid-item this">16:30</div>
	<div class="grid-item this">16:30</div>
	<div class="grid-item this">16:30</div>
	<div class="grid-item this">16:30</div>
	<div class="grid-item">16:30</div>
</div>

<style>
	.grid-container {
		display: grid;
		grid-template-columns: auto auto auto auto auto;
		background-color: #86c5f8;
		border-radius: 20px;
		padding: 20px;
		width: 40vw;
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

	.days {
		text-align: center;
		font-weight: bold;
		font-size: 16px;
	}

	.test {
		background-color: rgb(254, 155, 155);
	}
</style>