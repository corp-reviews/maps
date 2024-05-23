<!-- src/routes/+page.svelte -->

<script>
    import { onMount, onDestroy } from 'svelte';

    let map;

    // Function to initialize the map / 지도를 초기화하는 함수
    function initMap() {
        // Map options / 지도 옵션
        const options = {
            zoom: 10,
            center: { lat: 37.5665, lng: 126.9780 } // Center map on Seoul / 서울을 중심으로 지도 설정
        };

        // Create new map / 새 지도 생성
        map = new google.maps.Map(document.getElementById('map'), options);
    }

    // Load the map when the component is mounted / 컴포넌트가 마운트될 때 지도를 로드
    onMount(() => {
        // Track page view / 페이지 뷰 추적
        window.dataLayer = window.dataLayer || [];
        window.dataLayer.push({
            'event': 'pageview',
            'page': {
                'url': window.location.href,
                'title': document.title
            }
        });

        // Check if Google Maps API is loaded / Google Maps API가 로드되었는지 확인
        if (typeof google !== 'undefined' && google.maps) {
            initMap();
        } else {
            // Retry after a delay if the API is not loaded yet / API가 아직 로드되지 않았다면 지연 후 재시도
            const intervalId = setInterval(() => {
                if (typeof google !== 'undefined' && google.maps) {
                    clearInterval(intervalId);
                    initMap();
                }
            }, 1000);
        }
    });

    // Track page unload / 페이지 언로드 추적
    onDestroy(() => {
        window.dataLayer = window.dataLayer || [];
        window.dataLayer.push({
            'event': 'pageunload',
            'page': {
                'url': window.location.href,
                'title': document.title
            }
        });
    });
</script>

<div class="container mx-auto px-4 py-8 flex flex-col md:flex-row bg-gray-50 min-h-screen">
    <aside class="md:w-1/3 lg:w-1/4 bg-white p-6 rounded-lg shadow-md mb-8 md:mb-0 md:mr-8">
        <h1 class="text-4xl font-bold text-gray-800 mb-4">테크기업 찾기 지도</h1>
        <p class="text-lg text-gray-700 mb-6">구글맵 사용법:</p>
        <ul class="list-disc list-inside text-gray-700 mb-8 space-y-2">
            <li>레이어: 좌측 상단의 레이어 버튼을 사용하여 다양한 정보를 추가하세요.</li>
            <li>위치 검색: 지도 상단의 검색창을 이용해 원하는 위치를 검색하세요.</li>
            <li>길찾기: 특정 위치를 선택하고 길찾기 버튼을 클릭하세요.</li>
            <li>즐겨찾기 추가: 원하는 장소를 즐겨찾기에 추가하여 쉽게 찾을 수 있습니다.</li>
        </ul>
        <p class="text-lg text-gray-700 mb-6">How to use Google Maps:</p>
        <ul class="list-disc list-inside text-gray-700 space-y-2">
            <li>Layers: Use the layers button on the top left to add various information.</li>
            <li>Location Search: Use the search box at the top of the map to find the desired location.</li>
            <li>Directions: Select a specific location and click the directions button.</li>
            <li>Add to Favorites: Add desired places to your favorites for easy access.</li>
        </ul>
    </aside>

    <section class="md:w-2/3 lg:w-3/4 relative">
        <iframe 
            src="https://www.google.com/maps/d/u/0/embed?mid=1GiVhfp3KgnbYGz1xMNlPGgS4Egyb2hbM" 
            class="w-full h-screen md:h-[calc(100vh-64px)] rounded-lg shadow-md" 
            allowfullscreen>
        </iframe>
    </section>
</div>

<footer class="mt-8 text-center bg-gray-100 py-4">
    <p class="text-gray-600">
        View the source code on <a
            href="https://github.com/seoulcity/sveltekit_tailwindcss_supabase_bolierplate"
            target="_blank"
            rel="noopener noreferrer"
            class="text-blue-600 hover:underline">GitHub</a>
    </p>
    <p class="text-gray-600 text-sm mt-2">
        &copy; 2023 Kim JungHyun (<a
            href="https://linkedin.com/in/seoulite"
            target="_blank"
            rel="noopener noreferrer"
            class="text-blue-600 hover:underline">LinkedIn</a
        >) | Licensed under
        <a
            href="https://creativecommons.org/licenses/by/4.0/"
            target="_blank"
            rel="noopener noreferrer"
            class="text-blue-600 hover:underline">CC BY 4.0</a>
    </p>
</footer>
