    <template>
    <div class="flex flex-col gap-4 p-12 justify-center min-h-screen items-center">
        <!-- Кнопки выбора типа -->
        <div class="flex gap-4 flex-wrap justify-center">
        <label class="flex items-center gap-2 cursor-pointer hover:opacity-80">
            <input class="hidden" type="radio" value="all" v-model="selectedType" />
            <div class="w-16 h-16 flex items-center justify-center" :class="{ 'opacity-50': selectedType !== 'all'}"> 
            <span class="text-2xl font-bold">All</span>
            </div>
        </label>
        <label class="flex items-center gap-2 cursor-pointer hover:opacity-80">
            <input class="hidden" type="radio" value="agility" v-model="selectedType" />
            <img :src="'/images/hero_agility.png'" class="w-16 h-16" :class="{ 'opacity-50': selectedType !== 'agility' }" />
            <span class="text-xl font-semibold">Agility</span>
        </label>
        <label class="flex items-center gap-2 cursor-pointer hover:opacity-80">
            <input class="hidden" type="radio" value="intelligence" v-model="selectedType" />
            <img :src="'/images/hero_intelligence.png'" class="w-16 h-16" :class="{ 'opacity-50': selectedType !== 'intelligence' }" />
            <span class="text-xl font-semibold">Intelligence</span>
        </label>
        <label class="flex items-center gap-2 cursor-pointer hover:opacity-80">
            <input class="hidden" type="radio" value="strength" v-model="selectedType" />
            <img :src="'/images/hero_strength.png'" class="w-16 h-16" :class="{ 'opacity-50': selectedType !== 'strength' }" />
            <span class="text-xl font-semibold">Strength</span>
        </label>
        <label class="flex items-center gap-2 cursor-pointer hover:opacity-80">
            <input class="hidden" type="radio" value="universal" v-model="selectedType" />
            <img :src="'/images/hero_universal.png'" class="w-16 h-16" :class="{ 'opacity-50': selectedType !== 'universal' }" />
            <span class="text-xl font-semibold">Universal</span>
        </label>
        </div>

        <!-- Отображение героев выбранного типа -->
        <div class="flex flex-row gap-4 flex-wrap justify-center">
        <div class="hero-block" v-for="(hero, index) in filteredHeroes" :key="index">
            <img :src="hero.image" class="w-60 h-60 pt-2" :alt="hero.name" />
            <p class="text-xl">{{ hero.name }}</p>
        </div>
        </div>
    </div>
    </template>

    <script setup lang="ts">
    import { ref, computed } from 'vue'

    interface Hero {
    name: string
    image: string
    type: 'agility' | 'intelligence' | 'strength' | 'universal'
    }

    const heroes: Hero[] = [
    // Agility Heroes
    { name: 'Anti-Mage', image: '/images/hero_mini/anti-mage.png', type: 'agility' },
    { name: 'Arc Warden', image: '/images/hero_mini/arc warden.png', type: 'agility' },
    { name: 'Bloodseeker', image: '/images/hero_mini/bloodseeker.png', type: 'agility' },
    { name: 'Bounty Hunter', image: '/images/hero_mini/bounty hunter.png', type: 'agility' },
    { name: 'Broodmother', image: '/images/hero_mini/broodmother.png', type: 'agility' },
    { name: 'Clinkz', image: '/images/hero_mini/clinkz.png', type: 'agility' },
    { name: 'Drow Ranger', image: '/images/hero_mini/drow ranger.png', type: 'agility' },
    { name: 'Ember Spirit', image: '/images/hero_mini/ember spirit.png', type: 'agility' },
    { name: 'Faceless Void', image: '/images/hero_mini/faceless void.png', type: 'agility' },
    { name: 'Gyrocopter', image: '/images/hero_mini/gyrocopter.png', type: 'agility' },
    { name: 'Juggernaut', image: '/images/hero_mini/juggernaut.png', type: 'agility' },
    { name: 'Luna', image: '/images/hero_mini/luna.png', type: 'agility' },
    { name: 'Medusa', image: '/images/hero_mini/medusa.png', type: 'agility' },
    { name: 'Meepo', image: '/images/hero_mini/meepo.png', type: 'agility' },
    { name: 'Mirana', image: '/images/hero_mini/mirana.png', type: 'agility' },
    { name: 'Monkey King', image: '/images/hero_mini/monkey king.png', type: 'agility' },
    { name: 'Morphling', image: '/images/hero_mini/morphling.png', type: 'agility' },
    { name: 'Naga Siren', image: '/images/hero_mini/naga siren.png', type: 'agility' },
    { name: 'Nyx Assassin', image: '/images/hero_mini/nyx assassin.png', type: 'agility' },
    { name: 'Phantom Assassin', image: '/images/hero_mini/phantom assassin.png', type: 'agility' },
    { name: 'Phantom Lancer', image: '/images/hero_mini/phantom lancer.png', type: 'agility' },
    { name: 'Riki', image: '/images/hero_mini/riki.png', type: 'agility' },
    { name: 'Shadow Fiend', image: '/images/hero_mini/shadow fiend.png', type: 'agility' },
    { name: 'Slark', image: '/images/hero_mini/slark.png', type: 'agility' },
    { name: 'Sniper', image: '/images/hero_mini/sniper.png', type: 'agility' },
    { name: 'Spectre', image: '/images/hero_mini/spectre.png', type: 'agility' },
    { name: 'Templar Assassin', image: '/images/hero_mini/templar assassin.png', type: 'agility' },
    { name: 'Terrorblade', image: '/images/hero_mini/terrorblade.png', type: 'agility' },
    { name: 'Troll Warlord', image: '/images/hero_mini/troll warlord.png', type: 'agility' },
    { name: 'Ursa', image: '/images/hero_mini/ursa.png', type: 'agility' },
    { name: 'Vengeful Spirit', image: '/images/hero_mini/vengeful spirit.png', type: 'agility' },
    { name: 'Venomancer', image: '/images/hero_mini/venomancer.png', type: 'agility' },
    { name: 'Viper', image: '/images/hero_mini/viper.png', type: 'agility' },
    { name: 'Weaver', image: '/images/hero_mini/weaver.png', type: 'agility' },
    
    // Intelligence Heroes
    { name: 'Ancient Apparition', image: '/images/hero_mini/ancient apparition.png', type: 'intelligence' },
    { name: 'Bane', image: '/images/hero_mini/bane.png', type: 'intelligence' },
    { name: 'Batrider', image: '/images/hero_mini/batrider.png', type: 'intelligence' },
    { name: 'Chen', image: '/images/hero_mini/chen.png', type: 'intelligence' },
    { name: 'Crystal Maiden', image: '/images/hero_mini/crystal maiden.png', type: 'intelligence' },
    { name: 'Dark Seer', image: '/images/hero_mini/dark seer.png', type: 'intelligence' },
    { name: 'Dark Willow', image: '/images/hero_mini/dark willow.png', type: 'intelligence' },
    { name: 'Dazzle', image: '/images/hero_mini/dazzle.png', type: 'intelligence' },
    { name: 'Death Prophet', image: '/images/hero_mini/death prophet.png', type: 'intelligence' },
    { name: 'Disruptor', image: '/images/hero_mini/disruptor.png', type: 'intelligence' },
    { name: 'Enchantress', image: '/images/hero_mini/enchantress.png', type: 'intelligence' },
    { name: 'Enigma', image: '/images/hero_mini/enigma.png', type: 'intelligence' },
    { name: 'Grimstroke', image: '/images/hero_mini/grimstroke.png', type: 'intelligence' },
    { name: 'Invoker', image: '/images/hero_mini/invoker.png', type: 'intelligence' },
    { name: 'Jakiro', image: '/images/hero_mini/jakiro.png', type: 'intelligence' },
    { name: 'Keeper of the Light', image: '/images/hero_mini/keeper of the light.png', type: 'intelligence' },
    { name: 'Leshrac', image: '/images/hero_mini/leshrac.png', type: 'intelligence' },
    { name: 'Lich', image: '/images/hero_mini/lich.png', type: 'intelligence' },
    { name: 'Lina', image: '/images/hero_mini/lina.png', type: 'intelligence' },
    { name: 'Lion', image: '/images/hero_mini/lion.png', type: 'intelligence' },
    { name: 'Nature\'s Prophet', image: '/images/hero_mini/nature\'s prophet.png', type: 'intelligence' },
    { name: 'Necrophos', image: '/images/hero_mini/necrophos.png', type: 'intelligence' },
    { name: 'Oracle', image: '/images/hero_mini/oracle.png', type: 'intelligence' },
    { name: 'Outworld Destroyer', image: '/images/hero_mini/outworld destroyer.png', type: 'intelligence' },
    { name: 'Puck', image: '/images/hero_mini/puck.png', type: 'intelligence' },
    { name: 'Pugna', image: '/images/hero_mini/pugna.png', type: 'intelligence' },
    { name: 'Queen of Pain', image: '/images/hero_mini/queen of pain.png', type: 'intelligence' },
    { name: 'Rubick', image: '/images/hero_mini/rubick.png', type: 'intelligence' },
    { name: 'Shadow Demon', image: '/images/hero_mini/shadow demon.png', type: 'intelligence' },
    { name: 'Shadow Shaman', image: '/images/hero_mini/shadow shaman.png', type: 'intelligence' },
    { name: 'Silencer', image: '/images/hero_mini/silencer.png', type: 'intelligence' },
    { name: 'Skywrath Mage', image: '/images/hero_mini/skywrath mage.png', type: 'intelligence' },
    { name: 'Storm Spirit', image: '/images/hero_mini/storm spirit.png', type: 'intelligence' },
    { name: 'Tinker', image: '/images/hero_mini/tinker.png', type: 'intelligence' },
    { name: 'Visage', image: '/images/hero_mini/visage.png', type: 'intelligence' },
    { name: 'Warlock', image: '/images/hero_mini/warlock.png', type: 'intelligence' },
    { name: 'Windranger', image: '/images/hero_mini/windranger.png', type: 'intelligence' },
    { name: 'Winter Wyvern', image: '/images/hero_mini/winter wyvern.png', type: 'intelligence' },
    { name: 'Witch Doctor', image: '/images/hero_mini/witch doctor.png', type: 'intelligence' },
    { name: 'Zeus', image: '/images/hero_mini/zeus.png', type: 'intelligence' },
    
    // Strength Heroes
    { name: 'Abaddon', image: '/images/hero_mini/abaddon.png', type: 'strength' },
    { name: 'Alchemist', image: '/images/hero_mini/alchemist.png', type: 'strength' },
    { name: 'Axe', image: '/images/hero_mini/axe.png', type: 'strength' },
    { name: 'Beastmaster', image: '/images/hero_mini/beastmaster.png', type: 'strength' },
    { name: 'Brewmaster', image: '/images/hero_mini/brewmaster.png', type: 'strength' },
    { name: 'Bristleback', image: '/images/hero_mini/bristleback.png', type: 'strength' },
    { name: 'Centaur Warrunner', image: '/images/hero_mini/centaur warrunner.png', type: 'strength' },
    { name: 'Chaos Knight', image: '/images/hero_mini/chaos knight.png', type: 'strength' },
    { name: 'Clockwerk', image: '/images/hero_mini/clockwerk.png', type: 'strength' },
    { name: 'Dawnbreaker', image: '/images/hero_mini/dawnbreaker.png', type: 'strength' },
    { name: 'Doom', image: '/images/hero_mini/doom.png', type: 'strength' },
    { name: 'Dragon Knight', image: '/images/hero_mini/dragon knight.png', type: 'strength' },
    { name: 'Earth Spirit', image: '/images/hero_mini/earth spirit.png', type: 'strength' },
    { name: 'Earthshaker', image: '/images/hero_mini/earthshaker.png', type: 'strength' },
    { name: 'Elder Titan', image: '/images/hero_mini/elder titan.png', type: 'strength' },
    { name: 'Huskar', image: '/images/hero_mini/huskar.png', type: 'strength' },
    { name: 'Io', image: '/images/hero_mini/io.png', type: 'strength' },
    { name: 'Kunkka', image: '/images/hero_mini/kunkka.png', type: 'strength' },
    { name: 'Legion Commander', image: '/images/hero_mini/legion commander.png', type: 'strength' },
    { name: 'Lifestealer', image: '/images/hero_mini/lifestealer.png', type: 'strength' },
    { name: 'Lycan', image: '/images/hero_mini/lycan.png', type: 'strength' },
    { name: 'Magnus', image: '/images/hero_mini/magnus.png', type: 'strength' },
    { name: 'Marci', image: '/images/hero_mini/marci.png', type: 'strength' },
    { name: 'Mars', image: '/images/hero_mini/mars.png', type: 'strength' },
    { name: 'Night Stalker', image: '/images/hero_mini/night stalker.png', type: 'strength' },
    { name: 'Ogre Magi', image: '/images/hero_mini/ogre magi.png', type: 'strength' },
    { name: 'Omniknight', image: '/images/hero_mini/omniknight.png', type: 'strength' },
    { name: 'Phoenix', image: '/images/hero_mini/phoenix.png', type: 'strength' },
    { name: 'Primal Beast', image: '/images/hero_mini/primal beast.png', type: 'strength' },
    { name: 'Pudge', image: '/images/hero_mini/pudge.png', type: 'strength' },
    { name: 'Razor', image: '/images/hero_mini/razor.png', type: 'strength' },
    { name: 'Sand King', image: '/images/hero_mini/sand king.png', type: 'strength' },
    { name: 'Slardar', image: '/images/hero_mini/slardar.png', type: 'strength' },
    { name: 'Snapfire', image: '/images/hero_mini/snapfire.png', type: 'strength' },
    { name: 'Spirit Breaker', image: '/images/hero_mini/spirit breaker.png', type: 'strength' },
    { name: 'Sven', image: '/images/hero_mini/sven.png', type: 'strength' },
    { name: 'Techies', image: '/images/hero_mini/techies.png', type: 'strength' },
    { name: 'Tidehunter', image: '/images/hero_mini/tidehunter.png', type: 'strength' },
    { name: 'Timbersaw', image: '/images/hero_mini/timbersaw.png', type: 'strength' },
    { name: 'Tiny', image: '/images/hero_mini/tiny.png', type: 'strength' },
    { name: 'Treant Protector', image: '/images/hero_mini/treant protector.png', type: 'strength' },
    { name: 'Tusk', image: '/images/hero_mini/tusk.png', type: 'strength' },
    { name: 'Underlord', image: '/images/hero_mini/underlord.png', type: 'strength' },
    { name: 'Undying', image: '/images/hero_mini/undying.png', type: 'strength' },
    { name: 'Wraith King', image: '/images/hero_mini/wraith king.png', type: 'strength' },
    
    // Universal Heroes
    { name: 'Hoodwink', image: '/images/hero_mini/hoodwink.png', type: 'universal' },
    { name: 'Lone Druid', image: '/images/hero_mini/lone druid.png', type: 'universal' },
    { name: 'Muerta', image: '/images/hero_mini/muerta.png', type: 'universal' },
    { name: 'Pangolier', image: '/images/hero_mini/pangolier.png', type: 'universal' },
    { name: 'Void Spirit', image: '/images/hero_mini/void spirit.png', type: 'universal' },
    ]

    const selectedType = ref<'all' | 'agility' | 'intelligence' | 'strength' | 'universal'>('all')

    const filteredHeroes = computed(() => {
    if (selectedType.value === 'all') {
        return heroes
    }
    return heroes.filter(hero => hero.type === selectedType.value)
    })
    </script>

    <style scoped>
    .hero-block {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    border: 1px solid white;
    width: 18rem;
    height: auto;
    align-items: center;
    border-radius: 0.75rem;
    transition: all 0.3s;
    }

    .hero-block:hover {
    border-color: #eab308;
    background-color: rgba(0, 0, 0, 0.5);
    }
    </style>
