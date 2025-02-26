<script context="module" lang="ts">
	import type { Load } from '@sveltejs/kit';
	export const load: Load = async ({ fetch, session }) => {
		const url = `/dashboard.json`;
		const res = await fetch(url);

		if (res.ok) {
			return {
				props: {
					...(await res.json())
				}
			};
		}

		return {
			status: res.status,
			error: new Error(`Could not load ${url}`)
		};
	};
</script>

<script lang="ts">
	import { t } from '$lib/translations';

	export let applicationsCount: number;
	export let sourcesCount: number;
	export let destinationsCount: number;
	export let teamsCount: number;
	export let databasesCount: number;
	export let servicesCount: number;
</script>

<div class="flex space-x-1 p-6 font-bold">
	<div class="mr-4 text-2xl tracking-tight">{$t('index.dashboard')}</div>
</div>

<div class="mt-10 pb-12 tracking-tight sm:pb-16">
	<div class="relative">
		<div class="absolute inset-0 h-1/2" />
		<div class="relative mx-auto px-4 sm:px-6 lg:px-8">
			<div class="mx-auto max-w-4xl">
				<dl class="gap-5 gap-y-16 sm:grid sm:grid-cols-3">
					<a
						href="/applications"
						sveltekit:prefetch
						class="flex cursor-pointer flex-col rounded p-6 text-center text-green-500 no-underline transition duration-150 hover:bg-green-500 hover:text-white"
					>
						<dt class="order-2 mt-2 text-sm font-bold uppercase leading-6 text-white">
							{$t('index.applications')}
						</dt>
						<dd class="order-1 text-5xl font-extrabold ">
							{applicationsCount}
						</dd>
					</a>
					<a
						href="/destinations"
						sveltekit:prefetch
						class="flex cursor-pointer flex-col rounded p-6 text-center text-sky-500 no-underline transition duration-150 hover:bg-sky-500 hover:text-white"
					>
						<dt class="order-2 mt-2 text-sm font-bold uppercase leading-6 text-white">
							{$t('index.destinations')}
						</dt>
						<dd class="order-1 text-5xl font-extrabold ">
							{destinationsCount}
						</dd>
					</a>
					<a
						href="/sources"
						sveltekit:prefetch
						class="flex cursor-pointer flex-col rounded p-6 text-center text-orange-500 no-underline transition duration-150 hover:bg-orange-500 hover:text-white"
					>
						<dt class="order-2 mt-2 text-sm font-bold uppercase leading-6 text-white">
							{$t('index.git_sources')}
						</dt>
						<dd class="order-1 text-5xl font-extrabold ">
							{sourcesCount}
						</dd>
					</a>
					<a
						href="/databases"
						sveltekit:prefetch
						class="flex cursor-pointer flex-col rounded p-6 text-center text-purple-500 no-underline transition duration-150 hover:bg-purple-500 hover:text-white"
					>
						<dt class="order-2 mt-2 text-sm font-bold uppercase leading-6 text-white">
							{$t('index.databases')}
						</dt>
						<dd class="order-1 text-5xl font-extrabold ">{databasesCount}</dd>
					</a>
					<a
						href="/services"
						sveltekit:prefetch
						class="flex cursor-pointer flex-col rounded p-6 text-center text-pink-500 no-underline transition duration-150 hover:bg-pink-500 hover:text-white"
					>
						<dt class="order-2 mt-2 text-sm font-bold uppercase leading-6 text-white">
							{$t('index.services')}
						</dt>
						<dd class="order-1 text-5xl font-extrabold ">{servicesCount}</dd>
					</a>

					<a
						href="/iam"
						sveltekit:prefetch
						class="flex cursor-pointer flex-col rounded p-6 text-center text-cyan-500 no-underline transition duration-150 hover:bg-cyan-500 hover:text-white"
					>
						<dt class="order-2 mt-2 text-sm font-bold uppercase leading-6 text-white">
							{$t('index.teams')}
						</dt>
						<dd class="order-1 text-5xl font-extrabold ">
							{teamsCount}
						</dd>
					</a>
				</dl>
			</div>
		</div>
	</div>
</div>
