<template>
	<div class="bg-indigo-600 pb-32">
		<Disclosure
			as="nav"
			class="bg-indigo-600 border-b border-indigo-300 border-opacity-25 lg:border-none"
			v-slot="{ open }"
		>
			<div class="max-w-7xl mx-auto px-2 sm:px-4 lg:px-8">
				<div
					class="relative h-16 flex items-center justify-between lg:border-b lg:border-indigo-400 lg:border-opacity-25"
				>
					<div class="px-2 flex items-center lg:px-0">
						<Logo />
						<div class="hidden lg:block lg:ml-10">
							<div class="flex space-x-4">
								<!-- Current: "bg-indigo-700 text-white", Default: "text-white hover:bg-indigo-500 hover:bg-opacity-75" -->
								<RouterLink
									:to="item.to"
									v-for="(item, key) in navigation"
									:key="key"
									class="text-white rounded-md py-2 px-3 text-sm font-medium"
									:class="[routeName === item.name ? 'bg-indigo-700 ' : 'hover:bg-indigo-500 hover:bg-opacity-75']"
								>{{ item.name }}</RouterLink>
							</div>
						</div>
					</div>
					<div class="flex-1 px-2 flex justify-center lg:ml-6 lg:justify-end">
						<div class="max-w-lg w-full lg:max-w-xs">
							<label for="search" class="sr-only">Search</label>
							<div class="relative text-gray-400 focus-within:text-gray-600">
								<div class="pointer-events-none absolute inset-y-0 left-0 pl-3 flex items-center">
									<SearchIcon class="h-5 w-5" aria-hidden="true" />
								</div>
								<input
									id="search"
									class="block w-full bg-white py-2 pl-10 pr-3 border border-transparent rounded-md leading-5 text-gray-900 placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-indigo-600 focus:ring-white focus:border-white sm:text-sm"
									placeholder="Search"
									type="search"
									name="search"
								/>
							</div>
						</div>
					</div>
					<div class="flex lg:hidden">
						<!-- Mobile menu button -->
						<DisclosureButton
							class="bg-indigo-600 p-2 rounded-md inline-flex items-center justify-center text-indigo-200 hover:text-white hover:bg-indigo-500 hover:bg-opacity-75 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-indigo-600 focus:ring-white"
						>
							<span class="sr-only">Open main menu</span>
							<MenuIcon v-if="!open" class="block h-6 w-6" aria-hidden="true" />
							<XIcon v-else class="block h-6 w-6" aria-hidden="true" />
						</DisclosureButton>
					</div>
					<div class="hidden lg:block lg:ml-4">
						<div class="flex items-center">
							<!-- <button
								class="bg-indigo-600 flex-shrink-0 rounded-full p-1 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-indigo-600 focus:ring-white"
							>
								<span class="sr-only">View notifications</span>
								<BellIcon class="h-6 w-6" aria-hidden="true" />
							</button>-->
							<Notification />

							<!-- Profile dropdown -->
							<Menu as="div" class="ml-3 relative flex-shrink-0">
								<div>
									<MenuButton
										class="bg-indigo-600 rounded-full flex text-sm text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-indigo-600 focus:ring-white"
									>
										<span class="sr-only">Open user menu</span>
										<img
											class="rounded-full h-8 w-8"
											src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
											alt
										/>
									</MenuButton>
								</div>
								<transition
									enter-active-class="transition ease-out duration-100"
									enter-from-class="transform opacity-0 scale-95"
									enter-to-class="transform opacity-100 scale-100"
									leave-active-class="transition ease-in duration-75"
									leave-from-class="transform opacity-100 scale-100"
									leave-to-class="transform opacity-0 scale-95"
								>
									<MenuItems
										class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
									>
										<MenuItem v-for="(item, key) in profile" :key="key" v-slot="{ active }">
											<RouterLink
												:to="item.to"
												:class="[active ? 'bg-gray-100' : '', 'block py-2 px-4 text-sm text-gray-700']"
											>{{ item.title }}</RouterLink>
										</MenuItem>
										<MenuItem v-slot="{ active }" class="w-full">
											<button
												@click="signOut"
												:class="[active ? 'bg-gray-100' : '', 'text-left block py-2 px-4 text-sm text-gray-700']"
											>Sign out</button>
										</MenuItem>
									</MenuItems>
								</transition>
							</Menu>
						</div>
					</div>
				</div>
			</div>

			<DisclosurePanel class="lg:hidden">
				<div class="px-2 pt-2 pb-3 space-y-1">
					<!-- Current: "bg-indigo-700 text-white", Default: "text-white hover:bg-indigo-500 hover:bg-opacity-75" -->
					<RouterLink
						:to="item.to"
						v-for="(item, key) in navigation"
						:key="key"
						class="text-white block rounded-md py-2 px-3 text-base font-medium"
						:class="[routeName === item.name ? 'bg-indigo-700 ' : 'hover:bg-indigo-500 hover:bg-opacity-75']"
					>{{ item.name }}</RouterLink>
					<!-- <RouterLink
							:to="item.to"
							class="text-white hover:bg-indigo-500 hover:bg-opacity-75  rounded-md py-2 px-3 text-base font-medium"
					>{{ item.name }}</RouterLink>-->
				</div>
				<div class="pt-4 pb-3 border-t border-indigo-700">
					<div class="px-5 flex items-center">
						<div class="flex-shrink-0">
							<img
								class="rounded-full h-10 w-10"
								src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
								alt
							/>
						</div>
						<div class="ml-3">
							<div class="text-base font-medium text-white">Tom Cook</div>
							<div class="text-sm font-medium text-indigo-300">tom@example.com</div>
						</div>
						<button
							class="ml-auto bg-indigo-600 flex-shrink-0 rounded-full p-1 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-indigo-600 focus:ring-white"
						>
							<span class="sr-only">View notifications</span>
							<BellIcon class="h-6 w-6" aria-hidden="true" />
						</button>
					</div>
					<div class="mt-3 px-2 space-y-1">
						<RouterLink
							v-for="(item, key) in profile"
							:key="key"
							:to="item.to"
							class="block rounded-md py-2 px-3 text-base font-medium text-white hover:bg-indigo-500 hover:bg-opacity-75"
						>{{ item.title }}</RouterLink>
						<button
							@click="signOut"
							class="text-left w-full block rounded-md py-2 px-3 text-base font-medium text-white hover:bg-indigo-500 hover:bg-opacity-75 focus:outline-none"
						>Sign out</button>
					</div>
				</div>
			</DisclosurePanel>
		</Disclosure>
		<header class="py-10">
			<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
				<h1 class="text-3xl font-bold text-white">{{routeName}}</h1>
			</div>
		</header>
	</div>
</template>

<script>
	import {
		Disclosure,
		DisclosureButton,
		DisclosurePanel,
		Menu,
		MenuButton,
		MenuItem,
		MenuItems,
	} from "@headlessui/vue";
	import Notification from "@/components/loggedIn/Notification";
	import { SearchIcon } from "@heroicons/vue/solid";
	import { BellIcon, MenuIcon, XIcon } from "@heroicons/vue/outline";
    import Logo from '@/components/Logo'
	export default {
		data() {
			return {
				open: false,
				navigation: [
					{ name: "Dashboard", to: "/dashboard" },
					{ name: "Team", to: "/dashboard/team" },
					{ name: "Projects", to: "#" },
					{ name: "Calendar", to: "#" },
					{ name: "Reports", to: "#" },
				],
				profile: [
					{
						title: "Your Profile",
						to: "#",
					},
					{
						title: "Settings",
						to: "/settings",
					},
				],
			};
		},
		components: {
			Disclosure,
			DisclosureButton,
			DisclosurePanel,
			Menu,
			MenuButton,
			MenuItem,
			MenuItems,
			BellIcon,
			MenuIcon,
			SearchIcon,
			XIcon,
			Notification,
            Logo,
		},
		methods: {
			signOut() {
				this.$store.dispatch("auth/signOut");
			},
		},
		computed: {
			routeName() {
				return this.$route.name;
			},
		},
		created() {
			this.$store.dispatch("profile/getProfile");
		},
	};
</script>

<style>
</style>
