목사님, 2박 4일 일정으로 정확하게 수정했습니다.

수정 사항:

일정 변경: 2월 9일(월) 출발 ~ 2월 12일(목) 도착 (2박 4일)

귀국 편: 현지 시간 2월 12일(목) 새벽 01:30 출발로 반영했습니다. (즉, 수요일 밤에 공항으로 이동합니다.)

스케줄: 3일차(수)에 체크아웃 후 시내 관광을 하고 공항으로 바로 이동하는 꽉 찬 일정으로 조정했습니다.

수정된 전체 코드는 아래와 같습니다.

HTML
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2026 Nha Trang Retreat Dashboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700;900&display=swap');
        
        body {
            font-family: 'Noto Sans KR', sans-serif;
        }
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fadeIn {
            animation: fadeIn 0.4s ease-out forwards;
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-900">
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        // --- 아이콘 컴포넌트 ---
        const IconBase = ({ children, className, ...props }) => (
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className} {...props}>{children}</svg>
        );

        const Calendar = (props) => <IconBase {...props}><rect width="18" height="18" x="3" y="4" rx="2" ry="2"/><line x1="16" x2="16" y1="2" y2="6"/><line x1="8" x2="8" y1="2" y2="6"/><line x1="3" x2="21" y1="10" y2="10"/></IconBase>;
        const MapPin = (props) => <IconBase {...props}><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></IconBase>;
        const HeartHandshake = (props) => <IconBase {...props}><path d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/></IconBase>;
        const Users = (props) => <IconBase {...props}><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></IconBase>;
        const CheckSquare = (props) => <IconBase {...props}><polyline points="9 11 12 14 22 4"/><path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11"/></IconBase>;
        const Wallet = (props) => <IconBase {...props}><path d="M21 12V7a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v10a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2v-5Zm-6 0h6"/></IconBase>;
        const Clock = (props) => <IconBase {...props}><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></IconBase>;
        const Plane = (props) => <IconBase {...props}><path d="M2 22h20"/><path d="M13 6l6-4 2 2-6 4 6 4-2 2-6-4v6l-4 4v-4l-5 5-2-2 7-7V6z"/></IconBase>;
        const Cross = (props) => <IconBase {...props}><path d="M11 2a2 2 0 0 0-2 2v5H4a2 2 0 0 0-2 2v2c0 1.1.9 2 2 2h5v5c0 1.1.9 2 2 2h2a2 2 0 0 0 2-2v-5h5a2 2 0 0 0 2-2v-2a2 2 0 0 0-2-2h-5V4a2 2 0 0 0-2-2h-2z"/></IconBase>;
        const AlertTriangle = (props) => <IconBase {...props}><path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z"/><line x1="12" x2="12" y1="9" y2="13"/><line x1="12" x2="12.01" y1="17" y2="17"/></IconBase>;
        const MapIcon = (props) => <IconBase {...props}><polygon points="3 6 9 3 15 6 21 3 21 18 15 21 9 18 3 21"/><line x1="9" x2="9" y1="3" y2="18"/><line x1="15" x2="15" y1="6" y2="21"/></IconBase>;
        const ExternalLink = (props) => <IconBase {...props}><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" x2="21" y1="14" y2="3"/></IconBase>;
        const Sun = (props) => <IconBase {...props}><circle cx="12" cy="12" r="5"/><path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/></IconBase>;

        const MissionDashboard = () => {
            const [activeTab, setActiveTab] = useState('schedule');
            const [mapDay, setMapDay] = useState(1);

            // --- 데이터 섹션: 2박 4일 일정 반영 ---
            const tripData = {
                info: {
                    title: "2026 학생회 나트랑 수련회",
                    dates: "2026.02.09(월) - 02.12(목) [2박 4일]",
                    location: "베트남 나트랑 & 빈펄 리조트",
                    theme: "하나됨을 위한 쉼과 교제",
                    participants: {
                        members: 7,
                        details: "학생 및 교사 총 7명",
                        total: 7
                    }
                },
                schedule: [
                    {
                        day: "Day 1",
                        date: "2.09 (월)",
                        focus: "출국 및 도착",
                        timeline: [
                            { time: "06:15", activity: "인천공항 출발", type: "move" },
                            { time: "09:40", activity: "나트랑(깜란) 공항 도착", type: "move" },
                            { time: "11:00", activity: "시내 이동 및 환전", type: "move" },
                            { time: "12:00", activity: "점심: 쌀국수 맛집", type: "meal" },
                            { time: "14:00", activity: "빈펄 리조트 체크인 (2박)", type: "rest" },
                            { time: "16:00", activity: "리조트 수영 및 휴식", type: "rest" },
                            { time: "18:00", activity: "저녁: 리조트 내 식사", type: "meal" },
                            { time: "20:00", activity: "저녁 나눔 및 기도회", type: "worship" }
                        ]
                    },
                    {
                        day: "Day 2",
                        date: "2.10 (화)",
                        focus: "빈원더스 단합 활동",
                        timeline: [
                            { time: "08:00", activity: "기상 및 아침 큐티(QT)", type: "worship" },
                            { time: "09:30", activity: "빈원더스 이동", type: "move" },
                            { time: "10:00", activity: "오전: 워터파크 & 사파리", type: "active" },
                            { time: "13:00", activity: "점심 식사 (빈원더스 내)", type: "meal" },
                            { time: "14:00", activity: "오후: 놀이공원 & 아쿠아리움", type: "active" },
                            { time: "19:00", activity: "타타쇼 관람 (19:30)", type: "tour" },
                            { time: "20:30", activity: "저녁: 시내 이동 후 식사", type: "meal" },
                            { time: "22:00", activity: "빈펄 리조트 복귀", type: "rest" }
                        ]
                    },
                    {
                        day: "Day 3",
                        date: "2.11 (수)",
                        focus: "문화 탐방 및 출국 준비",
                        timeline: [
                            { time: "09:00", activity: "조식 및 짐 정리", type: "rest" },
                            { time: "11:00", activity: "체크아웃", type: "move" },
                            { time: "12:30", activity: "점심: 씀모이 가든", type: "meal" },
                            { time: "14:00", activity: "시내 관광 (포나가르/대성당)", type: "tour" },
                            { time: "16:00", activity: "롯데마트 기념품 쇼핑", type: "work" },
                            { time: "18:00", activity: "마지막 저녁 식사 (반세오)", type: "meal" },
                            { time: "20:00", activity: "전신 마사지 및 샤워", type: "rest" },
                            { time: "22:00", activity: "깜란 공항으로 이동", type: "move" }
                        ]
                    },
                    {
                        day: "Day 4",
                        date: "2.12 (목)",
                        focus: "귀국",
                        timeline: [
                            { time: "01:30", activity: "나트랑 출발 (비행기)", type: "move" },
                            { time: "08:30", activity: "인천공항 도착 및 해산", type: "move" }
                        ]
                    }
                ],
                budget: {
                    per_person: "약 980,000원 (항공포함)",
                    total: "약 6,850,000원 (7인)",
                    items: [
                        { category: "항공권", detail: "인천-나트랑 왕복 (7인, 1인 51만)", cost: "3,570,000원" },
                        { category: "숙박비", detail: "빈펄 리조트 2박 (3베드 풀빌라)", cost: "1,500,000원" },
                        { category: "식비", detail: "해산물, 현지식, 야시장, 간식", cost: "900,000원" },
                        { category: "활동비", detail: "빈원더스, 마사지 등", cost: "480,000원" },
                        { category: "교통비", detail: "공항 픽업/샌딩, 그랩", cost: "200,000원" },
                        { category: "예비비", detail: "비상금 및 기타", cost: "200,000원" }
                    ]
                },
                checklist: [
                    { id: 1, item: "여권 (유효기간 6개월 이상)", checked: false },
                    { id: 2, item: "달러/동 환전 (5만원권 or 100달러)", checked: false },
                    { id: 3, item: "Grab(그랩) 어플 설치", checked: false },
                    { id: 4, item: "샤워기 필터", checked: false },
                    { id: 5, item: "수영복 & 아쿠아슈즈", checked: false },
                    { id: 6, item: "선글라스, 선크림, 모자", checked: false },
                    { id: 7, item: "상비약 (소화제, 배탈약)", checked: false },
                    { id: 8, item: "성경책 및 나눔 노트", checked: false }
                ]
            };

            const mapLocations = {
                airport: { q: "Cam Ranh International Airport", label: "깜란 공항" },
                resort_area: { q: "Vinpearl Resort Nha Trang", label: "빈펄 리조트" },
                haisan: { q: "Hải sản Thanh Sương 2", label: "하이카2" },
                vinwonders: { q: "VinWonders Nha Trang", label: "빈원더스" },
                ponagar: { q: "Ponagar Temple", label: "포나가르 사원" },
                lotte: { q: "Lotte Mart Nha Trang", label: "롯데마트" },
                banhxeo: { q: "Bánh Xèo Chảo 85", label: "반세오" },
            };

            const dayRoutes = {
                1: { stops: ['airport', 'resort_area'], center: 'airport' },
                2: { stops: ['resort_area', 'vinwonders', 'resort_area'], center: 'vinwonders' },
                3: { stops: ['resort_area', 'ponagar', 'lotte', 'banhxeo', 'airport'], center: 'ponagar' },
                4: { stops: ['airport'], center: 'airport' }
            };

            const getGoogleMapUrl = (day) => {
                const route = dayRoutes[day] || dayRoutes[1];
                const centerLocation = mapLocations[route.center];
                return `https://maps.google.com/maps?q=$${encodeURIComponent(centerLocation.q)}&t=&z=12&ie=UTF8&iwloc=&output=embed`;
            };

            const getExternalMapUrl = (day) => {
                const route = dayRoutes[day] || dayRoutes[1];
                const query = route.stops.map(stopId => encodeURIComponent(mapLocations[stopId].q)).join('/');
                return `https://www.google.com/maps/dir/$${query}`;
            };

            const getTypeColor = (type) => {
                switch(type) {
                    case 'worship': return 'bg-purple-100 text-purple-700 border-purple-200';
                    case 'tour': return 'bg-blue-100 text-blue-700 border-blue-200';
                    case 'active': return 'bg-rose-100 text-rose-700 border-rose-200';
                    case 'meal': return 'bg-orange-50 text-orange-600 border-orange-100';
                    case 'rest': return 'bg-green-50 text-green-600 border-green-100';
                    case 'move': return 'bg-gray-100 text-gray-600 border-gray-200';
                    case 'work': return 'bg-yellow-50 text-yellow-700 border-yellow-200';
                    default: return 'bg-white text-gray-600 border-gray-100';
                }
            };

            const getTypeIcon = (type) => {
                switch(type) {
                    case 'worship': return <Cross className="w-4 h-4" />;
                    case 'tour': return <MapPin className="w-4 h-4" />;
                    case 'active': return <Sun className="w-4 h-4" />;
                    case 'meal': return <span className="text-xs font-bold">밥</span>;
                    case 'move': return <Plane className="w-4 h-4" />;
                    case 'work': return <Wallet className="w-4 h-4" />;
                    case 'rest': return <HeartHandshake className="w-4 h-4" />;
                    default: return <Clock className="w-4 h-4" />;
                }
            };

            const TabButton = ({ id, label, icon: Icon }) => (
                <button
                    onClick={() => setActiveTab(id)}
                    className={`flex items-center justify-center gap-2 py-3 px-3 text-sm font-bold rounded-xl transition-all duration-200 flex-1 sm:flex-none whitespace-nowrap
                        ${activeTab === id 
                         ? 'bg-emerald-600 text-white shadow-md shadow-emerald-200 transform -translate-y-0.5' 
                         : 'bg-white text-gray-500 hover:bg-gray-50 border border-transparent'}`}
                >
                    <Icon className="w-4 h-4" />
                    <span className="hidden sm:inline">{label}</span>
                </button>
            );

            const renderContent = () => {
                switch (activeTab) {
                    case 'schedule':
                        return (
                            <div className="space-y-6 animate-fadeIn">
                                {tripData.schedule.map((day, idx) => (
                                    <div key={idx} className="bg-white rounded-2xl p-5 shadow-sm border border-gray-100 overflow-hidden relative">
                                        <div className="flex justify-between items-center mb-4 border-b border-gray-100 pb-3">
                                            <div>
                                                <span className="text-xs font-bold text-emerald-600 bg-emerald-50 px-2 py-1 rounded-md mb-1 inline-block">{day.day}</span>
                                                <h3 className="text-lg font-bold text-gray-800">{day.date}</h3>
                                            </div>
                                            <div className="text-right">
                                                <span className="text-xs text-gray-400 font-medium">Focus</span>
                                                <p className="text-sm font-semibold text-gray-700">{day.focus}</p>
                                            </div>
                                        </div>
                                        <div className="space-y-3 relative">
                                            <div className="absolute left-[19px] top-2 bottom-2 w-0.5 bg-gray-100"></div>
                                            {day.timeline.map((item, tIdx) => (
                                                <div key={tIdx} className="flex items-start gap-3 relative z-10">
                                                    <div className="flex-shrink-0 w-10 text-xs font-medium text-gray-400 text-right pt-1.5 bg-white pr-1">
                                                        {item.time}
                                                    </div>
                                                    <div className={`flex-1 p-3 rounded-xl border flex items-center gap-3 ${getTypeColor(item.type)} shadow-sm`}>
                                                        <div className="opacity-70">
                                                            {getTypeIcon(item.type)}
                                                        </div>
                                                        <span className="text-sm font-medium">{item.activity}</span>
                                                    </div>
                                                </div>
                                            ))}
                                        </div>
                                    </div>
                                ))}
                            </div>
                        );
                    case 'map':
                        return (
                            <div className="animate-fadeIn">
                                <div className="bg-white rounded-2xl shadow-sm border border-gray-100 p-4 mb-4">
                                    <div className="flex justify-between items-center mb-4">
                                        <h3 className="font-bold text-gray-800 flex items-center gap-2">
                                            <MapPin className="w-5 h-5 text-emerald-600" />
                                            동선 지도
                                        </h3>
                                        <div className="flex bg-gray-100 rounded-lg p-1">
                                            {[1, 2, 3, 4].map(day => (
                                                <button
                                                    key={day}
                                                    onClick={() => setMapDay(day)}
                                                    className={`px-3 py-1 text-xs font-bold rounded-md transition-all ${mapDay === day ? 'bg-white text-emerald-600 shadow-sm' : 'text-gray-500'}`}
                                                >
                                                    D{day}
                                                </button>
                                            ))}
                                        </div>
                                    </div>
                                    <div className="relative w-full aspect-[4/3] bg-slate-100 rounded-xl overflow-hidden border border-slate-200 shadow-inner">
                                        <iframe
                                            width="100%"
                                            height="100%"
                                            frameBorder="0"
                                            scrolling="no"
                                            marginHeight="0"
                                            marginWidth="0"
                                            src={getGoogleMapUrl(mapDay)}
                                            className="w-full h-full"
                                            title={`Day ${mapDay} Map`}
                                        ></iframe>
                                    </div>
                                    <div className="mt-4">
                                        <a
                                            href={getExternalMapUrl(mapDay)}
                                            target="_blank"
                                            rel="noopener noreferrer"
                                            className="flex items-center justify-center gap-2 w-full py-3 bg-emerald-50 text-emerald-700 rounded-xl font-bold hover:bg-emerald-100 transition-colors border border-emerald-200"
                                        >
                                            <ExternalLink className="w-4 h-4" />
                                            Google Maps에서 전체 경로 열기
                                        </a>
                                    </div>
                                </div>
                            </div>
                        );
                    case 'budget':
                        return (
                            <div className="animate-fadeIn space-y-4">
                                <div className="bg-gradient-to-br from-cyan-500 to-blue-600 rounded-2xl p-6 text-white shadow-lg">
                                    <h3 className="text-lg font-medium opacity-90 mb-1">1인 예상 회비 (항공포함)</h3>
                                    <p className="text-3xl font-extrabold">{tripData.budget.per_person}</p>
                                    <div className="mt-4 pt-4 border-t border-white/20 flex justify-between items-center text-sm">
                                        <span className="opacity-80">총 예산 (7명 기준)</span>
                                        <span className="font-bold">{tripData.budget.total}</span>
                                    </div>
                                </div>
                                <div className="bg-white rounded-2xl shadow-sm border border-gray-100 overflow-hidden">
                                    <div className="p-4 bg-gray-50 border-b border-gray-100 font-bold text-gray-700 flex items-center gap-2">
                                        <Wallet className="w-4 h-4 text-emerald-600" />
                                        세부 산출 내역
                                    </div>
                                    <div className="divide-y divide-gray-50">
                                        {tripData.budget.items.map((item, idx) => (
                                            <div key={idx} className="p-4 flex justify-between items-center hover:bg-gray-50 transition-colors">
                                                <div>
                                                    <h4 className="font-bold text-gray-800 text-sm">{item.category}</h4>
                                                    <p className="text-xs text-gray-500 mt-0.5">{item.detail}</p>
                                                </div>
                                                <span className="font-medium text-emerald-600 text-sm">{item.cost}</span>
                                            </div>
                                        ))}
                                    </div>
                                </div>
                            </div>
                        );
                    case 'checklist':
                        return (
                            <div className="animate-fadeIn">
                                <div className="bg-white rounded-2xl shadow-sm border border-gray-100 p-6">
                                    <h3 className="font-bold text-gray-800 mb-4 flex items-center gap-2">
                                        <CheckSquare className="w-5 h-5 text-emerald-600" />
                                        준비물 체크리스트
                                    </h3>
                                    <div className="space-y-3">
                                        {tripData.checklist.map((item) => (
                                            <label key={item.id} className="flex items-center gap-3 p-3 rounded-xl border border-gray-100 cursor-pointer hover:bg-gray-50 transition-all active:scale-[0.99]">
                                                <input type="checkbox" className="w-5 h-5 rounded border-gray-300 text-emerald-600 focus:ring-emerald-500" />
                                                <span className="text-sm text-gray-700 font-medium select-none">{item.item}</span>
                                            </label>
                                        ))}
                                    </div>
                                </div>
                            </div>
                        );
                    default: return null;
                }
            };

            return (
                <div className="min-h-screen bg-gray-50 pb-20 max-w-md mx-auto shadow-2xl overflow-hidden min-h-[800px]">
                    <div className="bg-emerald-600 text-white p-6 pt-10 rounded-b-[2rem] shadow-lg relative overflow-hidden">
                        <div className="absolute top-0 right-0 p-10 opacity-10">
                            <Sun size={120} />
                        </div>
                        <div className="relative z-10">
                            <div className="flex items-center gap-2 mb-2 opacity-90">
                                <span className="bg-white/20 px-2 py-0.5 rounded text-xs font-bold">Retreat 2026</span>
                            </div>
                            <h1 className="text-2xl font-extrabold mb-1">Nha Trang Retreat</h1>
                            <p className="text-emerald-100 text-sm mb-4">2026 학생회 나트랑 수련회</p>
                            <div className="flex gap-4 text-xs font-medium bg-emerald-700/50 p-3 rounded-xl backdrop-blur-sm">
                                <div className="flex items-center gap-1.5">
                                    <Users className="w-3.5 h-3.5 opacity-70" />
                                    <span>총 {tripData.info.participants.total}명 (2박 4일)</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div className="px-4 -mt-6 relative z-20">
                        <div className="flex gap-2 overflow-x-auto no-scrollbar pb-2">
                            <TabButton id="schedule" label="일정표" icon={Calendar} />
                            <TabButton id="map" label="동선 지도" icon={MapIcon} />
                            <TabButton id="budget" label="예산" icon={Wallet} />
                            <TabButton id="checklist" label="준비물" icon={CheckSquare} />
                        </div>
                    </div>

                    <main className="px-4 py-4">
                        {renderContent()}
                    </main>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<MissionDashboard />);
    </script>
</body>
</html>
