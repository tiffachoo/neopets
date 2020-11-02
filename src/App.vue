<template>
	<div id="app">
		<div :class="{'nav-toggled': navToggled}" class="container">
			<header class="header">
				<button class="hamburger-button" @click="toggleNav">
					<span class="hamburger"></span>
				</button>
				<div class="header-left">neopets.com</div>
			</header>
			<nav class="side-nav">
				<ul class="nav-items">
					<li class="nav-item">
						<a id="petCentral" href="#" class="nav-link nav-link-main">
							<i class="nav-link-icon fas fa-home"></i>
							<span class="nav-link-text"><span class="lg">pet</span> <span class="md">central</span></span>
						</a>
					</li>
					<li class="nav-item">
						<a id="createPet" href="#" class="nav-link nav-link-main">
							<i class="nav-link-icon fas fa-paw"></i>
							<span class="nav-link-text"><span class="md">create</span> <span class="sm">a</span> <span class="lg">pet</span></span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-envelope"></i>
							<span class="nav-link-text">neomail</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-globe"></i>
							<span class="nav-link-text">world</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-star"></i>
							<span class="nav-link-text">explore</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-comments"></i>
							<span class="nav-link-text">chat</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-trophy"></i>
							<span class="nav-link-text">games</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-shopping-cart"></i>
							<span class="nav-link-text">shops</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-tv"></i>
							<span class="nav-link-text">news</span>
						</a>
					</li>
					<li class="nav-item">
						<a href="#" class="nav-link">
							<i class="nav-link-icon fas fa-question" data-fa-transform="shrink-10 up-1.25" data-fa-mask="fas fa-comment-alt"></i>
							<span class="nav-link-text">help</span>
						</a>
					</li>
					<li class="nav-item">
						<a id="login" href="#" class="nav-link">
							<i class="nav-link-icon fas fa-arrow-right"></i>
							<span class="nav-link-text">login!</span>
						</a>
					</li>
					<li class="nav-item">
						<a id="logout" href="#" class="nav-link">
							<i class="nav-link-icon fas fa-arrow-left"></i>
							<span class="nav-link-text">logout!</span>
						</a>
					</li>
					<li class="nav-item nav-item-ad">
						<img :src="`http://images.neopets.com/buttons/${getButton}.gif`" class="nav-ad">
					</li>
					<li id="user" class="nav-item nav-item-user">
						<span class="user-item">User: <a href="#" class="user-link">{{ user.name }}</a></span>
						<span class="user-item">Pet: <a href="#" class="user-link">{{ user.pet }}</a></span>
						<span class="user-item">NP: <a href="#" class="user-link">{{ user.np | formatCommas }}</a></span>
					</li>
					<li class="nav-item nav-item-form">
						<div class="form-container">
							<input type="text" class="form-control">
							<button class="button">Go</button>
						</div>
						<span class="nav-link-small">search neopets</span>
					</li>
					<li class="nav-item nav-item-form">
						<div class="form-select">
							<select class="form-control">
								<option>English</option>
								<option>French</option>
							</select>
						</div>
						<button class="button">Go</button><br>
						<span class="nav-link-small">Select Language</span>
					</li>
					<li class="nav-item nav-item-form">
						<a href="#" class="nav-link-small">link to us</a>
					</li>
				</ul>
			</nav>
			<main class="content">
				<section class="content-header">
					<div class="content-banner">
						<div class="content-banner-image" style="--banner-image: url('http://images.neopets.com/new_shopkeepers/t_418.gif')"></div>
						<span class="content-banner-header">user.lookup</span>
						<span class="content-banner-text-decor">whoareyou?</span>
					</div>
				</section>
				<section class="content-body">
					<h1>User Lookup: {{ username }}</h1>
					<div class="content-info">
						<div class="content-info-body">
							<ul>
								<li>
									<span class="content-info-title">Name:</span>
									{{ name }}
								</li>
								<li>
									<span class="content-info-title">Last Spotted:</span>
									{{ lastSpotted }}
								</li>
								<li>
									<span class="content-info-title">Gender:</span>
									<span :class="[`gender-${gender}`]">{{ gender }}</span>
								</li>
								<li>
									<span class="content-info-title">Country:</span>
									{{ country }}
								</li>
								<li>
									<span class="content-info-title">Started Playing:</span>
									{{ started.month }} {{ started.day }}, {{ started.year }}
								</li>
								<li v-if="shop">
									<span class="content-info-title">Shop:</span>
									<a href="#" class="content-info-link">{{ shop.name }}</a> (Size {{ shop.size }})
								</li>
								<li v-if="neodeck">
									<span class="content-info-title">NeoDeck:</span>
									<a href="#" class="content-info-link">{{ neodeck }}</a>
								</li>
								<li v-if="neohome">
									<span class="content-info-title">NeoHome:</span>
									<a href="#" class="content-info-link">{{ neohome }}</a>
								</li>
								<li v-if="guild.name">
									<span class="content-info-title">Guild Info:</span>
									{{ guild.rank }} in <a href="#" class="content-info-link">{{ guild.name }}</a>
								</li>
								<li v-if="battledome">
									<span class="content-info-title">One Player BD:</span>
									Won {{ battledome.wins }} out of {{ battledome.total }} ({{ calcBattledome }}%)
								</li>
								<li>
									<span class="content-info-title">Secret Avatars:</span>
									{{ avatars }}
								</li>
							</ul>
						</div>
						<div class="content-info-sheild">
							<img :src="`http://images.neopets.com/images/shields/${getSheild}.gif`" class="content-info-sheild-img">
						</div>
					</div>
					<div class="content-quick">
						<ul class="content-quick-items">
							<li class="content-quick-item">
								<a href="#" class="content-quick-link">
									<i class="content-quick-icon fas fa-sign"></i>
									<span class="content-quick-text">Trade</span>
								</a>
							</li>
							<li class="content-quick-item">
								<a href="#" class="content-quick-link">
									<i class="content-quick-icon fas fa-gavel"></i>
									<span class="content-quick-text">Auctions</span>
								</a>
							</li>
							<li class="content-quick-item">
								<a href="#" class="content-quick-link">
									<i class="content-quick-icon fas fa-gamepad"></i>
									<span class="content-quick-text">Scores ({{ scores }})</span>
								</a>
							</li>
							<li class="content-quick-item">
								<a href="#" class="content-quick-link">
									<i class="content-quick-icon fas fa-file-alt"></i>
									<span class="content-quick-text">Wishlist</span>
								</a>
							</li>
						</ul>
					</div>
					<div class="content-pets">
						<h2>Neopets</h2>
						<ul class="content-pets-items">
							<li 
								v-for="pet in pets" 
								:key="pet.name"
								class="content-pets-item"
							>
								<a href="#" class="content-pets-link">
									<img class="content-pets-img" :src="`http://images.neopets.com/pets/happy/${pet.species}_${pet.color}_baby.gif`">
									<span class="content-pets-text">{{ pet.name }}</span>
								</a>
								<span class="content-pets-text">
									<span :class="[`gender-${pet.gender}`]">{{ pet.gender }}</span> {{ pet.species }}
								</span>
								<span class="content-pets-text">
									Age: {{ getDays(pet.created) | formatCommas }} days
								</span>
								<span class="content-pets-text">
									Level: {{ pet.level }}
								</span>
							</li>
						</ul>
					</div>
					<hr>
					<div class="content-trophies">
						<div 
							v-for="(category, key) in trophies"
							:key="key"
						>
							<h2>{{ key }}</h2>
							<ul class="content-trophies-items">
								<li 
									v-for="trophy in category" 
									:key="trophy.text"
									class="content-trophies-item"
								>
									<img 
										:src="trophy.id ? `http://images.neopets.com/trophies/${trophy.id}_${trophy.place}.gif` : trophy.img" 
										class="content-trophies-img">
									<span v-if="trophy.place" :class="{'content-trophies-text-regular': trophy.place !== 1}" class="content-trophies-text">
										{{ getRankText(trophy.place, trophy.text) }}
									</span>
									<span v-else class="content-trophies-text">
										{{ trophy.text }}
									</span>
									<span v-if="trophy.points" class="content-trophies-text">
										{{ trophy.points }} points
									</span>
								</li>
							</ul>
						</div>
					</div>
				</section>
				<footer class="content-footer">
					<p></p>
				</footer>
			</main>
		</div>
	</div>
</template>

<script>
const data = {
	user: {
		name: 'kirby',
		pet: 'aisha',
		np: 25384
	},
	lookup: {
		username: 'kirby',
		name: 'tiff',
		gender: 'female',
		country: 'Canada',
		started: {
			day: 12,
			month: 'May',
			year: 2002
		},
		lastSpotted: 'Under one day ago',
		shop: {
			name: 'transparent',
			size: 5
		},
		gallery: {
			name: 'the science of fear',
			size: 55
		},
		neodeck: 'hello angel',
		neohome: '',
		battledome: {
			wins: 164,
			total: 188
		},
		guild: {
			name: '',
			rank: ''
		},
		avatars: 223,
		scores: 228,
		pets: [
			{
				name: 'aisha',
				species: 'aisha',
				color: 'shadow',
				gender: 'female',
				created: {
						day:  12,
						month: 'May',
						year: 2002
				},
				level: 20
			},
			{
				name: 'shoyru',
				species: 'shoyru',
				color: 'pirate',
				gender: 'female',
				created: {
					day: 12,
					month: 'May',
					year: 2002
				},
				level: 17
			},
			{
				name: 'draik',
				species: 'draik',
				color: 'ghost',
				gender: 'male',
				created: {
					day: 1,
					month: 'Dec',
					year: 2002
				},
				level: 22
			},
			{
				name: 'ixi',
				species: 'ixi',
				color: 'cloud',
				gender: 'female',
				created: {
					day: 30,
					month: 'Jul',
					year: 2002
				},
				level: 12
			}
		],
		trophies: {
			'Site Event': [
				{
					text: 'Serf',
					img: 'http://images.neopets.com/medieval/bfm_shield.gif',
					points: 5
				},
				{
					text: 'Expeditionist',
					img: 'http://images.neopets.com/winter/plot_hic/hic_hannah_2.gif',
					points: 52
				},
				{
					text: 'Cannoneer',
					img: 'http://images.neopets.com/water/plot_com/com_pirate_w_4.gif',
					points: 115
				},
				{
					text: 'Daily Dare 2009',
					img: 'http://images.neopets.com/games/aaa/trophies/2009/dd_trophies_1silver.gif'
				},
				{
					text: 'Atlas of the Ancients',
					img: 'http://images.neopets.com/aota/trophies/aota_trophy_1.gif'
				},
				{
					text: 'Battledome Veteran',
					img: 'http://images.neopets.com/dome/pages/bdtrophy_1.gif'
				}
			],
			'Site Feature': [
				{
					text: 'Defender of Neopia (Mission 4)',
					img: 'http://images.neopets.com/games/defenders/medal5_27475.gif'
				},
				{
					text: 'Lutari Talisman',
					img: 'http://images.neopets.com/mobile/talisman_80.gif'
				}
			],
			'Game': [
				{
					text: 'Snow Wars',
					place: 2,
					id: 55
				},
				{
					text: 'Pyramid Bonus',
					place: 3,
					id: 68
				},
				{
					text: 'Sakhmet Solitaire Bonus',
					place: 1,
					id: 77
				},
				{
					text: 'Go! Go! Go!',
					place: 3,
					id: 108
				},
				{
					text: 'Cheat!',
					place: 1,
					id: 109
				},
				{
					text: 'Beating Punchbag Bob',
					place: 1,
					id: 115
				},
				{
					text: 'Cellblock',
					place: 3,
					id: 216
				},
				{
					text: 'NeoQuest II',
					place: 3,
					id: 372
				},
				{
					text: 'Random Contest',
					place: 2,
					id: 479
				}
			]
		}
	}
};

export default {
	name: 'App',
	data() {
		return {
			user: data.user,
			...data.lookup,
			navToggled: false
		}
	},
	filters: {
		formatCommas(val) {
			return val.toString().replace(/(?=(\d{3})+(?!\d))/g, ',');
		}
	},
	computed: {
		calcBattledome() {
			return (this.battledome.wins / this.battledome.total * 100).toFixed(2);
		},
		getSheild() {
			const days = this.getDays(this.started);
			
			if (days >= 7 * 72) {
				let year = parseInt(days / 365);
				// const max = year > 15;
				const isMidYear = (days / 365) % 1 > 0.5;
				// year = max ? 15 : year;
				// return `${year}_${isMidYear || max ? 5 : 0}_years`
				return `${year}_${isMidYear ? 5 : 0}_years`
			} else if (days >= 7 * 4 && days < 7 * 72) {
				let month = parseInt(days / 30);
				month = month === 0 ? 1 : month;
				return `${month}mth`
			} else if (days >= 7 && days < 7 * 4) {
				const week = parseInt(days / 7);
				return `${week}wk`
			} else if (days >= 3 && days < 7) {
				return '3days'
			} else {
				return 'newbie'
			}
		},
		getButton() {
			const ads = [
				'message_120x60',
				'button_bd2',
				'button_bd1',
				'islandbanner3',
				'islandbanner4',
				'smallishgorm',
				'bingo_120x60'
			];
			const random = Math.floor(Math.random() * ads.length)
			return ads[random];
		}
	},
	methods: {
		getRankText(place, text) {
			switch (place) {
				case 1: 
					return `${text} CHAMPION!!!`
				case 2:
					return `Second place at ${text}!!`
				default:
					return `Third place at ${text}!!`
			}
		},
		getDays(val) {
			const today = new Date();
			const startDate = new Date(`${val.day} ${val.month} ${val.year}`);
			const diff = today - startDate;
			return this.convertDays(diff);
		},
		convertDays(val) {
			return parseInt(val / (1000 * 60 * 60 * 24))
		},
		toggleNav() {
			this.navToggled = !this.navToggled;
		}
	}
}
</script>

<style lang="scss">
@import '@/styles/reset';
@import '@/styles/styles';
</style>
