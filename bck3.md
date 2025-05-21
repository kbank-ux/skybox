<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<link rel="apple-touch-icon" sizes="57x57" href="assets/apple-icon-57x57.png">
	<link rel="apple-touch-icon" sizes="60x60" href="assets/apple-icon-60x60.png">
	<link rel="apple-touch-icon" sizes="72x72" href="assets/apple-icon-72x72.png">
	<link rel="apple-touch-icon" sizes="76x76" href="assets/apple-icon-76x76.png">
	<link rel="apple-touch-icon" sizes="114x114" href="assets/apple-icon-114x114.png">
	<link rel="apple-touch-icon" sizes="120x120" href="assets/apple-icon-120x120.png">
	<link rel="apple-touch-icon" sizes="144x144" href="assets/apple-icon-144x144.png">
	<link rel="apple-touch-icon" sizes="152x152" href="assets/apple-icon-152x152.png">
	<link rel="apple-touch-icon" sizes="180x180" href="assets/apple-icon-180x180.png">
	<link rel="icon" type="image/png" sizes="192x192"  href="assets/android-icon-192x192.png">
	<link rel="icon" type="image/png" sizes="32x32" href="assets/favicon-32x32.png">
	<link rel="icon" type="image/png" sizes="96x96" href="assets/favicon-96x96.png">
	<link rel="icon" type="image/png" sizes="16x16" href="assets/favicon-16x16.png">
	<link rel="manifest" href="assets/manifest.json">
	<meta name="msapplication-TileColor" content="#ffffff">
	<meta name="msapplication-TileImage" content="assets/ms-icon-144x144.png">
	<meta name="theme-color" content="#ffffff">
	<title>대망의 럭키드로우!!</title>
	<style lang="scss">
		* {
			box-sizing: border-box;
		}

		canvas {
			position: fixed;
			inset: 0;
			width: 100%;
			height: 100%;
		}

		div.copyright {
			position: fixed;
			bottom: 0;
			left: 50%;
			transform: translateX(-50%);
			color: white;
			font-size: 12px;
			z-index: 999;
		}

		div.copyright a {
			color: white;
		}

		#pageTitle {
			position: fixed;           
			top: 20px;                 
			left: 50%;                 
			transform: translateX(-50%);
			color: white;              
			font-size: clamp(16px, 4vw, 36px); /* 반응형 폰트 크기 설정 */
			font-weight: bold;         
			z-index: 9999;             
			margin: 0;
			padding: 0 00px; /* 좌우 패딩을 늘려 공간을 넓힘 */
			text-align: center;
			width: 80%; /* div의 폭을 더 넓게 설정 */
			white-space: normal; /* 텍스트가 여러 줄로 표시될 수 있도록 설정 */
			line-height: 1.2; /* 줄 간격 조정 */
		}


		#countdownOverlay {
			position: fixed;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
			display: none;
			align-items: center;
			justify-content: center;
			background: rgba(0, 0, 0, 0.5); /* 반투명 배경 (필요시) */
			z-index: 99999; /* 최상위로 올려서 다른 요소 위에 표시 */
			font-size: 100px;
			color: white;
			font-weight: bold;
			text-align: center;
		}
		#entryPool, #selectedPool {
			position: fixed;
			top: 0;
			left: 0;
			right: 0;
			bottom: 0;
			border: 1px solid #ccc;
			padding: 10px;
			margin: 10px;
			height: 200px;
			overflow-y: auto;
			z-index: 0; /* 최상위로 올려서 다른 요소 위에 표시 */
			background: rgba(0, 0, 0, 0.5); /* 반투명 배경 (필요시) */
			}
		.selected {
		color: green;
		font-weight: bold;
		transition: transform 0.3s, opacity 0.3s;
		}
		.fading {
		opacity: 0;
		transform: scale(0.5);
		transition: transform 0.5s, opacity 0.5s;
		}

		#settings {
			position: fixed;
			bottom: 1rem;
			left: 1rem;
			background: #666;
			border-radius: 10px;
			padding: 10px;
			z-index: 999;
			min-width: 50%;

			display: flex;
			visibility: visible;
			opacity: 1;
			transition: visibility 0s, opacity 1s linear;
			&.hide {
				opacity: 0;
				visibility: hidden;
			}

			h3 {
				padding:0;
				margin: 0;
				font-size: 12pt;
				color: #fefefe;
			}

			textarea {
				width: 100%;
				min-height: 5rem;
				border: none;
				background: #999;
				font-size: 14pt;
			}

			button {
				color: #fefefe;
				background: #222;
				border: none;
				border-radius: 5px;
				padding: 5px 10px;
				position: relative;
				overflow: hidden;
				&:active:after {
					content: '';
					position: absolute;
					left: 0;
					top: 0;
					right: 0;
					bottom: 0;
					background: rgba(0, 0, 0, 0.5);
				}
			}

			.icon {
				background: currentColor;
				mask-repeat: no-repeat;
				mask-position: center center;
				mask-size: contain;
				display: inline-block;
				width: 25px;
				height: 25px;
				vertical-align: middle;
				&.play {
					mask-image: url('assets/images/play.svg');
				}
				&.shuffle {
					mask-image: url('assets/images/shuffle.svg');
				}
				&.record {
					mask-image: url('assets/images/record.svg');
				}
				&.map {
					mask-image: url('assets/images/map.svg');
				}
				&.trophy {
					mask-image: url('assets/images/trophy.svg');
				}
				&.bomb {
					mask-image: url('assets/images/bomb.svg');
				}
				&.preplay {
					mask-image: url('assets/images/check.svg');
				}
			}

			div.left {
				flex-grow: 1;
				flex-shrink: 1;
				order: 1;
				.actions {
					text-align: right;
				}
			}
			div.right {
				order: 2;
				flex-grow: 0;
				flex-shrink: 0;

				div.row {
					display: flex;
					align-items: center;
					height: 35px;
					label {
						width: 150px;
						flex-grow: 0;
						flex-shrink: 0;
						padding-left: 1rem;
						color: white;
					}
				}
			}

			select {
				height: 25px;
				width: 100%;
				border-radius: 5px;
				background: #999;
			}

			input[type=checkbox] {
				width: 0;
				height: 25px;
				position: relative;
				vertical-align: middle;
				&:before {
					position: absolute;
					content: '';
					display: inline-block;
					width: 50px;
					height: 25px;
					border-radius: 25px;
					background: #999;
					top: 0;
					left: 0;
				}
				&:after {
					position: absolute;
					top: 0;
					left: 0;
					content: '';
					border-radius: 25px;
					width: 25px;
					height: 25px;
					background: #ccc;
					transition: transform .2s;
				}
				&:checked:after {
					transform: translateX(100%);
					background: white;
				}
				&:checked:before {
					content: '';
					background: #00baff;
				}
			}

			.btn-group {
				display: flex;
				justify-content: stretch;
				&>* {
					box-sizing: border-box;
					flex-grow: 0;
					flex-shrink: 0;
					overflow: hidden;
					height: 25px;
					width: 33%;
					border-radius: 0;
					background: #999;
					border: none;
					padding: 0;
					color: #fefefe;

					display: flex;
					align-items: center;
					justify-content: center;

					&:first-child {
						border-radius: 10px 0 0 10px;
					}
					&:last-child {
						border-radius: 0 10px 10px 0;
					}
					&.active:before {
						content: '';
						width: 15px;
						height: 15px;
						display: inline-block;
						vertical-align: middle;
						mask-image: url('assets/images/check.svg');
						mask-repeat: no-repeat;
						background: white;
					}
					&.active {
						background: #333;
					}
				}
				input[type=number] {
					box-sizing: border-box;
					text-align: center;
				}
			}
		}

		#donate {
			position: fixed;
			bottom: calc(160px + 1.5rem);
			left: 1rem;
			z-index: 999;
			visibility: visible;
			opacity: 1;
			transition: visibility 0s, opacity 1s linear;
			&.hide {
				opacity: 0;
				visibility: hidden;
			}
		}

		@media screen and (max-width: 750px) {
			#donate {
				bottom: 1rem;
			}
			#settings {
				bottom: calc(1.5rem + 60px);
				display: block;
				min-width: 0;
				max-width: 100%;
				width: calc(100% - 2rem);
				overflow: hidden;
				opacity: 1;
				visibility: visible;
				transition: visibility 0s, opacity 1s linear;
				&.hide {
					opacity: 0;
					visibility: hidden;
				}
				div.right div.row {
					height: auto;
					display: block;
					border-bottom: 1px solid #555;
					padding: .5rem 0;

					label {
						width: 100%;
						margin-bottom: .5rem;
						padding-left: 0;
						display: block;
					}

					.icon {
						width: 15px;
						height: 15px;
					}
				}
			}
		}
	</style>
</head>
<body>
<audio id="backgroundMusic" src="assets/conan.mp3" loop></audio>
<script type="module" src="./src/index.ts"></script>
<script type="text/javascript">

	window.startBackgroundMusic = function() {
		var audio = document.getElementById('backgroundMusic');
		if (audio) {
			audio.muted = false; // 음소거 해제
			audio.play().then(() => {
			}).catch((error) => {
				console.log('Error playing audio:', error);
			});
		} else {
			console.log('Audio element not found.');
		}
	}
	window.startCountdown = function(callback) {
		const overlay = document.getElementById('countdownOverlay');
		overlay.style.display = 'flex'; // 카운트다운 시작 시 표시

		const messages = ['3', '2', '1', 'GO!'];
		let index = 0;

		// 메시지를 순차적으로 표시하는 함수
		function showMessage() {
			if (index < messages.length) {
				overlay.textContent = messages[index];
				index++;
				setTimeout(showMessage, 1000); // 다음 메시지를 1초 후에 표시
			} else {
				// 마지막 메시지("GO!")를 1초 동안 표시한 후 오버레이 숨김 및 콜백 실행
				setTimeout(() => {
					overlay.style.display = 'none';
					callback(); // 카운트다운 완료 후 콜백 호출 (룰렛 시작)
				}, 10);
			}
		}

		showMessage(); // 카운트다운 시작
	}

	window.dataLayer = window.dataLayer || [];
	// function gtag(){dataLayer.push(arguments);}
	// gtag('js', new Date());
	// gtag('config', 'G-5899C1DJM0');

	function getNames() {
		const value = document.querySelector('#in_names').value.trim();
		return value.split(/[,\r\n]/g).map(v => v.trim()).filter(v => !!v);
	}

	function parseName(nameStr) {
		const weightRegex = /(\/\d+)/;
		const countRegex = /(\*\d+)/;
		const hasWeight = weightRegex.test(nameStr);
		const hasCount = countRegex.test(nameStr);
		const name = /^\s*([^\/*]+)?/.exec(nameStr)[1];
		const weight = hasWeight ? parseInt(weightRegex.exec(nameStr)[1].replace('/', '')) : 1;
		const count = hasCount ? parseInt(countRegex.exec(nameStr)[1].replace('*', '')) : 1;
		return {
			name,
			weight,
			count,
		};
	}

	// function getReady() {
	// 	const names = getNames();
	// 	window.roullete.setMarbles(names);
	// 	ready = names.length > 0;
	// 	localStorage.setItem('mbr_names', names.join(','));
	// 	switch(winnerType) {
	// 		case 'first':
	// 			setWinnerRank(1);
	// 			break;
	// 		case 'last':
	// 			const total = window.roullete.getCount();
	// 			setWinnerRank(total);
	// 			break;
	// 	}
	// }


	function startDraw() {
		const entryPool = document.getElementById("entryPool");
		const selectedPool = document.getElementById("selectedPool");
		const names = getNames(); // 기존의 이름 리스트 가져오기

		// 최대 샘플링 수
		const MAX_SAMPLES = 10;

		// 1. 이름 풀 생성: 이름*숫자를 처리하여 이름 풀(expandedNames)을 만듭니다.
		const expandedNames = names.flatMap((name) => {
			const match = name.match(/^(.*)\*(\d+)$/); // "이름*숫자" 패턴 확인
			if (match) {
			const baseName = match[1].trim();
			const count = parseInt(match[2], 10);
			return Array(count).fill(baseName); // 이름을 숫자만큼 확장
			}
			return [name.trim()]; // "이름"만 있는 경우 그대로 추가
		});

		// 2. 샘플링을 위한 초기화
		const sampledNames = [];
		let remainingNames = [...expandedNames];

		// UI 초기화
		entryPool.innerHTML = expandedNames
			.map((name) => `<div class="name">${name}</div>`)
			.join("");
		selectedPool.innerHTML = "";

		function drawName() {
			if (sampledNames.length >= MAX_SAMPLES || remainingNames.length === 0) {
			// 3. 응모 완료 메시지
			alert("1차 응모가 완료되었습니다!");
			return;
			}

			// 4. 랜덤으로 하나의 이름 선택
			const randomIndex = Math.floor(Math.random() * remainingNames.length);
			const selectedName = remainingNames.splice(randomIndex, 1)[0];

			// 5. DOM에서 해당 이름 요소 가져오기
			const nameElements = [...entryPool.children];
			const nameElement = nameElements[randomIndex];

			if (!nameElement) {
			console.error("No matching element found for the selected name.");
			return;
			}

			// 6. 선택된 이름에 애니메이션 추가 및 이동
			nameElement.classList.add("fading");
			setTimeout(() => {
			nameElement.remove();
			}, 500);

			// 7. 선택된 이름을 결과 리스트에 추가
			sampledNames.push(selectedName);
			const newElement = document.createElement("div");
			newElement.textContent = selectedName;
			newElement.classList.add("selected");
			selectedPool.appendChild(newElement);

			// 8. 다음 이름 뽑기
			setTimeout(drawName, 100); // 100ms 간격으로 뽑기
		}

		drawName();
		}


	function getReady() {
		const names = getNames();

		// 최대 공 생성 수
		const MAX_MARBLES = 50;

		// 이름을 확장 (e.g., "Alice*3" -> ["Alice", "Alice", "Alice"])
		const expandedNames = names.flatMap((name) => {
			const match = name.match(/^(.*)\*(\d+)$/); // "이름*숫자" 패턴 확인
			if (match) {
				const baseName = match[1].trim();
				const count = parseInt(match[2], 10);
				return Array(count).fill(baseName); // 이름을 숫자만큼 확장
			}
			return name.trim(); // "이름"만 있는 경우 그대로 반환
		});

		// 랜덤 샘플링하여 최대 공 생성 수만큼 이름 선택
		const limitedNames =
			expandedNames.length > MAX_MARBLES
				? expandedNames.sort(() => Math.random() - 0.5).slice(0, MAX_MARBLES)
				: expandedNames;

		// window.roullete.setMarbles에 이름 리스트만 전달
		window.roullete.setMarbles(limitedNames);

		// 준비 상태 업데이트
		ready = limitedNames.length > 0;
		localStorage.setItem('mbr_names', limitedNames.join(',')); // 제한된 이름 리스트 저장

		// 기존 로직 유지
		switch (winnerType) {
			case 'first':
				setWinnerRank(1);
				break;
			case 'last':
				const total = window.roullete.getCount();
				setWinnerRank(total);
				break;
		}
	}


	// function getReady() {
	// 	const names = getNames();

	// 	// 최대 공 생성 수
	// 	const MAX_MARBLES = 10;

	// 	// 이름이 MAX_MARBLES보다 많으면 샘플링
	// 	const limitedNames =
	// 		names.length > MAX_MARBLES
	// 		? names.sort(() => Math.random() - 0.5).slice(0, MAX_MARBLES)
	// 		: names;

	// 	window.roullete.setMarbles(limitedNames);

	// 	ready = limitedNames.length > 0;
	// 	localStorage.setItem('mbr_names', limitedNames.join(','));

	// 	// 나머지 로직 유지
	// 	switch (winnerType) {
	// 		case 'first':
	// 		setWinnerRank(1);
	// 		break;
	// 		case 'last':
	// 		const total = window.roullete.getCount();
	// 		setWinnerRank(total);
	// 		break;
	// 	}
	// }

	function setWinnerRank(rank) {
		document.querySelector('#in_winningRank').value = rank;
		window.options.winningRank = rank - 1;
		window.roullete.setWinningRank(window.options.winningRank);

		if (winnerType === 'first') {
			document.querySelector('.btn-first-winner').classList.toggle('active', true);
			document.querySelector('.btn-last-winner').classList.toggle('active', false);
			document.querySelector('#in_winningRank').classList.toggle('active', false);
		} else if (winnerType === 'last') {
			document.querySelector('.btn-first-winner').classList.toggle('active', false);
			document.querySelector('.btn-last-winner').classList.toggle('active', true);
			document.querySelector('#in_winningRank').classList.toggle('active', false);
		} else if (winnerType === 'custom') {
			document.querySelector('.btn-first-winner').classList.toggle('active', false);
			document.querySelector('.btn-last-winner').classList.toggle('active', false);
			document.querySelector('#in_winningRank').classList.toggle('active', true);
		}
	}


	let ready = false;
	let winnerType = 'first';

	localStorage.removeItem('mbr_names');

	document.addEventListener('DOMContentLoaded', () => {
		initialize();
	});
	function initialize() {
		if (!window.roullete || !window.roullete.isReady) {
			console.log('does not loaded yet');
			setTimeout(initialize, 100);
			return;
		}
		console.log('initializing start');

		const savedNames = localStorage.getItem('mbr_names');
		if (savedNames) {
			document.querySelector('#in_names').value = savedNames;
		}
		document.querySelector('#in_names').addEventListener('input', () => {
			getReady();
		});

		document.querySelector('#in_names').addEventListener('blur', () => {
			const nameSource = getNames();
			const nameSet = new Set();
			const nameCounts = {};
			nameSource.forEach(nameSrc => {
				const name = parseName(nameSrc);
				const key = name.weight > 1 ? `${name.name}/${name.weight}` : name.name;
				if (!nameSet.has(key)) {
					nameSet.add(key);
					nameCounts[key] = 0;
				}
				nameCounts[key] += name.count;
			});
			const result = [];
			Object.keys(nameCounts).forEach(key => {
				if (nameCounts[key] > 1) {
					result.push(`${key}*${nameCounts[key]}`);
				} else {
					result.push(key);
				}
			});

			const oldValue = document.querySelector('#in_names').value;
			const newValue = result.join(',');

			if (oldValue !== newValue) {
				document.querySelector('#in_names').value = newValue;
				getReady();
			}
		});


		document.querySelector('#btnPreStart').addEventListener('click', () => {
			startDraw();
		});

		document.querySelector('#btnShuffle').addEventListener('click', () => {
			getReady();
		});

		document.querySelector('#btnStart').addEventListener('click', () => {
			if (!ready) return;
			// gtag && gtag('event', 'start', {
			// 	'event_category': 'roulette',
			// 	'event_label': 'start',
			// 	'value': window.roullete.getCount(),
			// });
			window.startBackgroundMusic(); 
			startCountdown(() => {
				// 카운트다운 완료 후 실행할 내용
				window.roullete.start();
				document.querySelector('#settings').classList.add('hide');
			});
			document.querySelector('#settings').classList.add('hide');
			//document.querySelector('#donate').classList.add('hide');
		});

		window.options.autoRecording = true;
		window.roullete.setAutoRecording(window.options.autoRecording);

		document.querySelector('#chkAutoRecording').addEventListener('change', (e) => {
			window.options.autoRecording = e.target.matches(':checked');
			window.roullete.setAutoRecording(window.options.autoRecording);
		});

		window.options.useSkills = false;
		window.roullete.setWinningRank(window.options.winningRank);

		document.querySelector('#chkSkill').addEventListener('change', (e) => {
			window.options.useSkills = e.target.matches(':checked');
			window.roullete.setWinningRank(window.options.winningRank);
		});

		document.querySelector('#in_winningRank').addEventListener('change', (e) => {
			const v = parseInt(e.target.value, 10);
			winnerType = 'custom';
			setWinnerRank(isNaN(v) ? 0 : v);
		});

		document.querySelector('.btn-last-winner').addEventListener('click', () => {
			const total = window.roullete.getCount();
			winnerType = 'last';
			setWinnerRank(total);
		});
		document.querySelector('.btn-first-winner').addEventListener('click', () => {
			winnerType = 'first';
			setWinnerRank(1);
		});

		document.querySelector('#btnShake').addEventListener('click', () => {
			window.roullete.shake();
			gtag('event', 'shake', {
				'event_category': 'roulette',
				'event_label': 'shake',
				'value': 1,
			});
		});

		window.roullete.addEventListener('goal', () => {
			ready = false;
			setTimeout(() => {
				document.querySelector('#settings').classList.remove('hide');
				//document.querySelector('#donate').classList.remove('hide');
			}, 3000);
		});

		window.roullete.addEventListener('shakeAvailableChanged', (e) => {
			document.querySelector('#inGame').classList.toggle('hide', !e.detail);
		});

		document.querySelector('#btnShuffle').click();

		const maps = window.roullete.getMaps();
		const mapSelector = document.querySelector('#sltMap');
		maps.forEach((map) => {
			const option = document.createElement('option');
			option.value = map.index;
			option.innerHTML = map.title;
			option.setAttribute('data-trans', '');
			window.translateElement(option);
			mapSelector.append(option);
		});
		mapSelector.addEventListener('change', (e) => {
			const index = e.target.value;
			window.roullete.setMap(index);
		});

		const checkDonateButtonLoaded = () => {
			const btn = document.querySelector('span.bmc-btn-text');
			if (!btn) {
				setTimeout(checkDonateButtonLoaded, 100);
			} else {
				console.log('donation button has been loaded');
				btn.setAttribute('data-trans', '');
				window.translateElement(btn);
			}
		};
		//setTimeout(checkDonateButtonLoaded, 100);
	}
</script>
<h1 id="pageTitle">12월 소통미팅, <br>근데 이제 럭키드로우를 곁들인</h1>
<div id="settings" class="settings">
	<div class="right">
		<div class="row">
			<label>
				<i class="icon map"></i>
				<span data-trans>Map</span>
			</label>
			<select id="sltMap"></select>
		</div>
		<div class="row">
			<label>
				<i class="icon record"></i>
				<span data-trans>Recording</span>
			</label>
			<input type="checkbox" id="chkAutoRecording" checked />
		</div>
		<div class="row">
			<label>
				<i class="icon trophy"></i>
				<span data-trans>The winner is</span>
			</label>
			<div class="btn-group">
				<button class="btn-winner btn-first-winner active" data-trans>First</button>
				<button class="btn-winner btn-last-winner" data-trans>Last</button>
				<input type="number" id="in_winningRank" value="1" min="1" />
			</div>
		</div>
		<div class="row">
			<label>
				<i class="icon bomb"></i>
				<span data-trans>Using skills</span>
			</label>
			<input type="checkbox" id="chkSkill" />
		</div>
	</div>
	<div class="left">
		<h3 data-trans>Enter names below</h3>
		<textarea id="in_names" placeholder="Input names separated by commas or line feed here" data-trans="placeholder">김정의*25,양지혜*24,윤혜지*24,최훈진*24,이예린*23,한희창*22,배재빈*22,강영훈*21,김민석(혁신서비스개발팀)*21,김지은(혁신서비스개발팀)*21,김훈희*21,정제용*21,조영남*21,최선필*21,남규환*21,한우탁*21,권혁주*20,이경진*20,배성학*20,이성진*20,신예빈*20,김혜민(여신정책팀)*20,권준태*20,남정유*19,조유숙*19,강희원*19,김성무*18,조희정*16,반준우*15,이희주*15,도승훈*15,이상림*15,이스완*15,이창수*15,홍서연*15,이진영(뱅킹서비스개발팀)*15,이수민*15,맹소연*15,강병재*15,박선희*14,김평중*14,이미진*14,김여진*14,김현*14,김현준*14,우예은*14,김기수*14,신다혜*14,이누리*14,정창현*14,김수연*14,조상아*14,오영운*14,안귀남*14,한효주*14,박명진*14,박서현*14,유미*14,신지혜*14,이은지*14,조혜원*13,이영숙*12,허윤경*12,김성령*12,이종우*12,하성호*12,최두완*11,변지애*11,이명호*11,지수연*11,변소윤*11,차영민*11,김채원*11,송호경*11,류진규*11,김영환*11,이미화*11,최유*11,홍민지*11,김재동*10,최정성*10,김홍종*10,박지인*10,김원경*10,이종벽*10,최서영*10,양재혁*10,이원종*10,이지원*10,안정훈*10,정의석*10,박정은*10,최수진*10,김민석(수신팀)*10,장지은*10,김수용*9,이명근*9,정종윤*9,이승규*9,김성아*9,이승진*9,김종민*9,정겨운*9,양사록*9,김형준*9,고태훈*9,이민섭*9,이태희*9,정재웅*9,이진영(UX팀)*9,김범철*9,김민지(회계팀)*9,정유나*9,강진수*9,이지완*9,김진우*9,김재철*8,윤소정*8,노은애*8,양재석*7,강인조*7,허찬일*7,김영록*7,고은아*7,원다연*7,경기환*6,정동윤*6,권기현*6,권혁민*6,김한준*6,김민영*6,방승욱*6,이규민*6,오수경*6,현윤선*6,김주희*6,오준엽*6,이태경*5,김윤지*5,김미리*5,신현준*5,오충현*5,김재익*5,석은록*5,최혜원(개발기획팀)*5,김세영*5,김하영*5,고금락*5,허동규*5,정민호*5,최미리*5,서승희*5,김은지*5,노은정*5,정희도*5,장현주*5,박수민*5,현용환*5,서원대*5,김지용*5,김혜민(여신플랫폼개발팀)*5,이관열*5,이송현*5,신수민*5,최윤정(법무팀)*5,이찬주*5,김지연(IT기획팀)*5,윤혜정*5,최민수*5,김보성*5,조선경*5,진보성*5,이상엽*5,윤지선*5,이성현*5,한완규*5,안효권*5,김선경*5,김송현*5,김진식*5,이지연*5,한지연*5,정지수*5,양민호*5,김정훈*5,김태응*5,윤혜선*4,이다정*4,김별*4,방지은*4,신수경*4,고영민*4,변정*4,손수길*4,문준성*4,이소연*4,공도승*4,이정구*4,김화원*4,정지황*4,김효식*4,윤혜령*4,김담이*4,문재용*4,채준식*4,고시철*4,하윤영*4,조효진*4,박은지*4,김희주*4,이가영*4,김태림*4,신한별*4,김지영*4,백준상*4,김정민*4,이경민*4,이정규*4,송우현*4,이순배*4,이범희*4,김우영*4,최병학*4,정희준*4,최창환*4,김소연*4,이경호*4,최성재*4,이진*4,박수미*4,김진옥*4,조민구*4,정다은*4,조승빈*4,장준혁*4,이자영*4,박진형*4,이아영*4,김혜은*4,서호현*4,양희진*4,김부년*4,이선화*4,김대의*4,함희란*4,조한정*4,김호영*4,서지오*4,이현정*4,홍원택*4,김수현*4,강동현*4,이준범*4,원지은*4,방사현*4,안상영*4,변우혁*4,최윤정(여신플랫폼개발팀)*4,정태성*4,김경서*4,오민석*4,권재현*4,정은정*4,고상문*4,박장표*4,김가회*4,강윤지*4,나태호*4,이동엽*2,구예은*2,김혜원*2,박세아*2,여주운*2,김보현*2,성명기*2,정성목*2,김예림*2,이강병*2,김형욱*2,박효선*2,조융*2,천한식*2,박순명*2,김문성*2,이유리*2,주윤정*2,김선교*2,정지원*2,김현수*2,박정진*2,차재형*2,이용배*2,김준우*2,임광진*2,이지은*2,김연정*2,김동욱*2,김지수*2,이재훈*2,성종현*2,최용범*2,최승호(리스크관리팀)*2,박희재*2,박윤아*2,김인철*2,안지환*2,조상현*2,이하연*2,김영명*2,최영락*2,김민지(BX팀)*2,최원영*2,문지현*2,윤혁준*2,조성호*2,이푸름*2,양준모*2,허철*2,윤승재*2,심어진*2,이진우*2,이지현*2,윤채영*2,오현아*2,조상원*2,조철*2,윤우현*2,이루리*2,최승호(경영기획팀)*2,이찬하*2,양동원*2,박우진*2,함지우*2,이승민*2,최우형*1,강병주*1,김경수*1,황석하*1,민재서*1,노수경*1,곽기은*1,이동원*1,정희진*1,허선미*1,기유림*1,김지석*1,김영관*1,이동규*1,김성미*1,박성원*1,원성호*1,양준영*1,이윤수*1,한정은*1,현주경*1,박민욱*1,박지은*1,노효준*1,민경은*1,왕우정*1,홍민수*1,전제원*1,문찬익*1,최민아*1,김은우*1,김민찬*1,한명수*1,최인철*1,이상윤*1,백달*1,최영태*1,박준현*1,류헌*1,여운중*1,허유정*1,최은지*1,문지홍*1,이연주*1,이지윤*1,김수림*1,김유경*1,이재은*1,조예문*1,이창선*1,이소정*1,김도희*1,장혜원*1,백봉아*1,이상현*1,조용걸*1,박다혜*1,김철기*1,김보경*1,김수진*1,남인수*1,김은채*1,손준우*1,오호진*1,강태호*1,김성민*1,강지웅*1,황현록*1,김민경*1,최진열*1,이상용*1,황선아*1,임양수*1,전재원*1,김지은(금융서비스팀)*1,김용민*1,정예진*1,박미라*1,한성준*1,심유정*1,김한아*1,김서경*1,최수정*1,김상훈*1,강윤서*1,유근영*1,박준오*1,차대산*1,이현숙*1,이정욱*1,노윤정*1,송인욱*1,석보현*1,승민주*1,이재황*1,성병무*1,조성남*1,황범순*1,백창훈*1,윤지훈*1,정병윤*1,하진관*1,박민수*1,안규진*1,임태훈*1,최재혁*1,송정현*1,김우성*1,김종진*1,김정연*1,최주덕*1,허시영*1,최광현*1,이현식*1,이관우*1,한정희*1,김성진(IT인프라팀)*1,김건록*1,유병훈*1,정하니*1,안지은*1,전수빈*1,안지원*1,이은상*1,이준영*1,박영록*1,김남석*1,전경철*1,박원석*1,김준호*1,한동기*1,김태수*1,이대헌*1,홍인의*1,김원익*1,유의성*1,나영열*1,심재엽*1,서한길*1,김재성*1,이주영*1,전정현*1,박혜미*1,장우석*1,서예찬*1,이아르미*1,박형구*1,박진균*1,윤맑은이슬*1,류현수*1,오주영*1,고선영*1,전종상*1,박수용*1,박채영*1,박성경*1,김가윤*1,김성진(뱅킹플랫폼팀)*1,문현이*1,김재형*1,차진영*1,홍민호*1,정주현*1,박승연*1,강영웅*1,이다운*1,정준영*1,김하윤*1,진소희*1,김현민*1,오승철*1,정의헌*1,이요한*1,박종영*1,이진욱*1,장인우*1,양영태*1,김경아*1,김신중*1,황서진*1,육창현*1,임경택*1,이민형*1,김경륜*1,우정은*1,윤석규*1,김수린*1,조지현*1,이재준*1,이준형*1,정현숙*1,성민현*1,변승철*1,김미현*1,이형준*1,김정은*1,구태운*1,이승환*1,김희진*1,육두수*1,윤승욱*1,이주원*1,이재영*1,김지연(재무기획팀)*1,신우주*1,진병권*1,김동우*1,탁윤성*1,김기영*1,채지영*1,이수연*1,권고운*1,김한울*1,김성호*1,이예은*1,박유림*1,이도훈*1,허은재*1,박현준*1,김미향*1,김명철*1,전현주*1,장정화*1,정민영*1,이성수*1,임재일*1,이영지*1,김다솜*1,이유한*1,전만풍*1,이권희*1,박세준*1,손소영*1,최혜원(AML팀)*1,신선애*1,박하윤*1,남의진*1,박건우*1,지하늘*1,김유림*1,김솔비*1,하정인*1,최정은*1,백재연*1,김희정*1,정다와*1,윤다나*1,장호성*1,조연아*1,김홍진*1,호규찬*1,채병서*1</textarea>
		<div class="actions">
			<button id="btnShuffle">
				<i class="icon shuffle"></i>
				<span data-trans>Shuffle</span>
			</button>
			<button id="btnPreStart">
				<i class="icon preplay"></i>
				<span data-trans>1차 선별</span>
			</button>
			<button id="btnStart">
				<i class="icon play"></i>
				<span data-trans>Start</span>
			</button>
		</div>
	</div>
</div>

<div id="entryPool">
	응모자
	<!-- 초기 이름 리스트 -->
  </div>
  <div id="selectedPool">
	1차 통자
	<!-- 선택된 이름 리스트 -->
  </div>
  
<div id="countdownOverlay"></div>
<div id="inGame" class="settings hide">
	<button id="btnShake" data-trans>Shake!</button>
</div>
<div class="copyright"></div> 원작자 : lazygyu</a></div>
</body>
</html>
