<script>
    import { onMount } from 'svelte';
    import {writable} from 'svelte/store';
    import {Alert, Card} from 'flowbite-svelte';
    import { InfoCircleSolid } from 'flowbite-svelte-icons';



    const array = writable([]); // Initialize as an empty array

    onMount(async () => {
        try {
            const response = await fetch('https://rumor-lab.com/goods/lowPrice'); // API 엔드포인트를 여기에 추가하세요.
            if (response.ok) {
                const data = await response.json();
                array.set(data); // 불러온 데이터를 array 스토어에 설정합니다.
            } else {
                console.error('Failed to fetch data');
            }
        } catch (error) {
            console.error('Error fetching data:', error);
        }
    });

    let goods; // 데이터를 저장할 변수

    // array 스토어를 구독하여 데이터에 접근
    array.subscribe(value => {
        goods = value;
    });
</script>

<style>
    .card-grid {
        display: grid;
        grid-template-columns: repeat(2, 1fr); /* 두 칸으로 나누기 */
        gap: 16px; /* 그리드 아이템 사이의 간격 설정 */
    }

    .card-text {
        display: flex;
        flex-direction: row;
        align-items: center;
        text-align: center;
    }
</style>

<figure class="flex flex-col justify-center items-center p-8 text-center bg-white rounded-t-lg border-b border-gray-200 md:rounded-t-none md:rounded-tl-lg md:border-r dark:bg-gray-800 dark:border-gray-700">

    <Alert border color="dark" class="m-5">
        <InfoCircleSolid slot="icon" class="w-4 h-4" />
        <span class="font-medium"></span>
        금일 최저가 아이템을 보여줍니다
    </Alert>

    <div class="card-grid">
        {#each goods as data}
            <Card class="inline-block w-48">
                <div class="flex flex-col items-center pb-1">
                    <div class="card-text">
                        <h5 class="mb-1 text-xl font-medium text-gray-900 dark:text-white">{data.name}</h5>
                    </div>

                    <img size="lg" src="{data.image}"/> <!-- 이미지 데이터를 사용하려면 data.image를 사용합니다. -->

                    <span class="text-sm text-gray-900 dark:text-gray-400">Amount: {data.amount}</span>
                    <div class="card-text mt-2">
                        <span class="ml-2 text-sm text-gray-500 dark:text-gray-400">{data.description}</span>
                    </div>

                    <div class="card-text mt-4">
                        <span class="flex items-center text-xl font-medium text-gray-900 relative">
                            <img src="/walk.jpeg" alt="Your Icon" class="h-4 w-4 mr-1" />
                            {data.price}
                        </span>
                    </div>
                </div>
            </Card>
        {/each}
    </div>
</figure>