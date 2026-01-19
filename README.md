import React, { useState, useEffect } from 'react';
import { 
  Calendar, 
  Clock, 
  Video, 
  CheckCircle, 
  BookOpen, 
  Youtube, 
  FileText, 
  Layout, 
  Bot, 
  Users, 
  MonitorPlay,
  ArrowRight,
  Sparkles,
  AlertCircle,
  Menu,
  X
} from 'lucide-react';

const AishLandingPage = () => {
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [timeLeft, setTimeLeft] = useState({ days: 0, hours: 0, minutes: 0, seconds: 0 });
  const [formData, setFormData] = useState({
    name: '',
    phone: '',
    email: '',
    course: 'all' // Default to all or specific selection
  });
  const [showSuccess, setShowSuccess] = useState(false);

  // 카운트다운 로직 (2026년 1월 30일 마감 기준 예시)
  useEffect(() => {
    const targetDate = new Date("2026-01-30T23:59:59").getTime();
    
    const interval = setInterval(() => {
      const now = new Date().getTime();
      const distance = targetDate - now;
      
      if (distance < 0) {
        clearInterval(interval);
      } else {
        setTimeLeft({
          days: Math.floor(distance / (1000 * 60 * 60 * 24)),
          hours: Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
          minutes: Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60)),
          seconds: Math.floor((distance % (1000 * 60)) / 1000)
        });
      }
    }, 1000);

    return () => clearInterval(interval);
  }, []);

  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setFormData({ ...formData, [name]: value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // 실제 데이터 전송 로직이 들어갈 곳
    console.log('Form Submitted:', formData);
    setShowSuccess(true);
    setTimeout(() => setShowSuccess(false), 3000);
  };

  const scrollToSection = (id) => {
    setIsMenuOpen(false);
    document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
  };

  const curriculum = [
    {
      id: 1,
      title: "정부과제 사업계획서 마스터",
      desc: "AI를 활용하여 승률 높은 사업계획서를 작성하는 전문가 노하우",
      icon: <FileText className="w-8 h-8 text-blue-600" />
    },
    {
      id: 2,
      title: "유튜브 CF 영상 제작",
      desc: "기획부터 편집까지, 우리 회사 제품 홍보 영상 뚝딱 만들기",
      icon: <Youtube className="w-8 h-8 text-red-600" />
    },
    {
      id: 3,
      title: "5주 완성 전자책 출간",
      desc: "교보문고에 내 이름으로 된 책을 등록하는 퍼스널 브랜딩의 정점",
      icon: <BookOpen className="w-8 h-8 text-green-600" />
    },
    {
      id: 4,
      title: "1시간 완성 랜딩페이지",
      desc: "코딩 없이 AI로 고객을 끌어당기는 홈페이지 제작 실습",
      icon: <Layout className="w-8 h-8 text-purple-600" />
    },
    {
      id: 5,
      title: "AI 업무자동화 에이전트",
      desc: "반복 업무는 이제 그만! 나만의 AI 비서 만들기",
      icon: <Bot className="w-8 h-8 text-indigo-600" />
    },
    {
      id: 6,
      title: "Notebook LM 제안서/강의안",
      desc: "구글 Notebook LM으로 방대한 자료를 순식간에 요약하고 생성",
      icon: <Sparkles className="w-8 h-8 text-yellow-500" />
    },
    {
      id: 7,
      title: "구글 워크스페이스 정복",
      desc: "이메일, 드라이브, 제미나이 연동으로 스마트워크 완전 정복",
      icon: <Users className="w-8 h-8 text-blue-400" />
    },
    {
      id: 8,
      title: "AI 홍보영상 올인원",
      desc: "미드저니, 캔바, 제미나이를 융합한 고퀄리티 영상 제작",
      icon: <MonitorPlay className="w-8 h-8 text-pink-500" />
    }
  ];

  return (
    <div className="font-sans text-gray-800 bg-white">
      {/* Navigation */}
      <nav className="fixed w-full z-50 bg-white/90 backdrop-blur-md border-b border-gray-100 shadow-sm">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex justify-between items-center h-16">
            <div className="flex-shrink-0 flex items-center gap-2 cursor-pointer" onClick={() => window.scrollTo(0,0)}>
              <div className="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center text-white font-bold">A</div>
              <span className="font-bold text-xl tracking-tight text-slate-900">AISH 교육협회</span>
            </div>
            
            {/* Desktop Menu */}
            <div className="hidden md:flex space-x-8 items-center">
              <button onClick={() => scrollToSection('about')} className="text-gray-600 hover:text-blue-600 font-medium">과정소개</button>
              <button onClick={() => scrollToSection('curriculum')} className="text-gray-600 hover:text-blue-600 font-medium">커리큘럼</button>
              <button onClick={() => scrollToSection('schedule')} className="text-gray-600 hover:text-blue-600 font-medium">일정안내</button>
              <button 
                onClick={() => scrollToSection('apply')}
                className="bg-blue-600 text-white px-6 py-2 rounded-full font-bold hover:bg-blue-700 transition shadow-lg hover:shadow-blue-500/30"
              >
                지금 신청하기
              </button>
            </div>

            {/* Mobile Menu Button */}
            <div className="md:hidden flex items-center">
              <button onClick={() => setIsMenuOpen(!isMenuOpen)} className="text-gray-600">
                {isMenuOpen ? <X size={24} /> : <Menu size={24} />}
              </button>
            </div>
          </div>
        </div>

        {/* Mobile Menu */}
        {isMenuOpen && (
          <div className="md:hidden bg-white border-t border-gray-100 absolute w-full">
            <div className="px-2 pt-2 pb-3 space-y-1 sm:px-3">
              <button onClick={() => scrollToSection('about')} className="block w-full text-left px-3 py-2 text-gray-600 font-medium">과정소개</button>
              <button onClick={() => scrollToSection('curriculum')} className="block w-full text-left px-3 py-2 text-gray-600 font-medium">커리큘럼</button>
              <button onClick={() => scrollToSection('schedule')} className="block w-full text-left px-3 py-2 text-gray-600 font-medium">일정안내</button>
              <button onClick={() => scrollToSection('apply')} className="block w-full text-left px-3 py-2 text-blue-600 font-bold">지금 신청하기</button>
            </div>
          </div>
        )}
      </nav>

      {/* Hero Section */}
      <header className="relative pt-24 pb-16 lg:pt-32 lg:pb-24 bg-slate-900 overflow-hidden">
        <div className="absolute inset-0 opacity-20 bg-[url('https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80')] bg-cover bg-center"></div>
        <div className="absolute inset-0 bg-gradient-to-br from-slate-900 via-blue-900/80 to-slate-900"></div>
        
        <div className="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <div className="inline-block px-4 py-1.5 rounded-full bg-blue-500/20 border border-blue-400/30 text-blue-300 font-semibold text-sm mb-6 animate-fade-in-up">
            AISH 중급 과정 회원 전용 스페셜 클래스
          </div>
          <h1 className="text-4xl md:text-6xl font-extrabold text-white tracking-tight mb-6 leading-tight">
            AI 교육, 듣기만 하고 끝내시겠습니까?<br/>
            <span className="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-emerald-400">
              5주 만에 '결과'를 만드는 전문가
            </span>가 되십시오.
          </h1>
          <p className="mt-4 max-w-2xl mx-auto text-xl text-gray-300 mb-10">
            정부과제 사업계획서부터 전자책 출간, 홍보영상 제작까지.<br className="hidden md:block" />
            단순 수강이 아닌, 내 이름으로 된 결과물을 만드는 <strong>실전 훈련 과정</strong>입니다.
          </p>
          
          <div className="flex flex-col sm:flex-row gap-4 justify-center items-center">
            <button 
              onClick={() => scrollToSection('apply')}
              className="w-full sm:w-auto px-8 py-4 bg-blue-600 text-white rounded-xl font-bold text-lg hover:bg-blue-500 transition shadow-lg shadow-blue-600/30 flex items-center justify-center gap-2"
            >
              수강 신청하기 <ArrowRight size={20} />
            </button>
            <button 
              onClick={() => scrollToSection('curriculum')}
              className="w-full sm:w-auto px-8 py-4 bg-white/10 backdrop-blur-sm text-white border border-white/20 rounded-xl font-bold text-lg hover:bg-white/20 transition"
            >
              커리큘럼 보기
            </button>
          </div>

          <div className="mt-12 p-6 bg-white/5 backdrop-blur-md rounded-2xl border border-white/10 inline-block">
             <p className="text-sm text-blue-200 mb-2 font-medium">접수 마감까지 남은 시간</p>
             <div className="flex justify-center gap-4 text-white font-mono text-2xl md:text-3xl font-bold">
               <div className="text-center">
                 <div className="bg-slate-800 rounded p-2 min-w-[60px]">{timeLeft.days}</div>
                 <div className="text-xs text-gray-400 mt-1 font-sans">일</div>
               </div>
               <div className="self-start py-2">:</div>
               <div className="text-center">
                 <div className="bg-slate-800 rounded p-2 min-w-[60px]">{timeLeft.hours}</div>
                 <div className="text-xs text-gray-400 mt-1 font-sans">시간</div>
               </div>
               <div className="self-start py-2">:</div>
               <div className="text-center">
                 <div className="bg-slate-800 rounded p-2 min-w-[60px]">{timeLeft.minutes}</div>
                 <div className="text-xs text-gray-400 mt-1 font-sans">분</div>
               </div>
             </div>
          </div>
        </div>
      </header>

      {/* Problem & Solution Section */}
      <section id="about" className="py-20 bg-gray-50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div>
              <h2 className="text-base text-blue-600 font-bold tracking-wide uppercase mb-2">Why This Course?</h2>
              <h3 className="text-3xl font-bold text-gray-900 mb-6">
                배우기만 하고<br/>
                적용하지 못하는 AI는<br/>
                죽은 지식입니다.
              </h3>
              <div className="space-y-4 text-gray-600 text-lg">
                <p>
                  많은 분들이 AI 툴 사용법을 배우지만, 정작 실무에 적용하여 성과를 내는 단계에서 멈칫합니다.
                </p>
                <div className="bg-white p-4 rounded-lg shadow-sm border-l-4 border-red-500 italic">
                  "홈페이지를 만들어야 하는데..."<br/>
                  "전자책을 쓰고 싶은데..."<br/>
                  "정부지원 사업계획서는 막막하고..."
                </div>
                <p className="font-semibold text-gray-900 pt-2">
                  AISH 스페셜 과정은 이 고민을 5주 만에 해결합니다.
                </p>
              </div>
              <ul className="mt-8 space-y-3">
                {[
                  "이론 중심이 아닌 100% 실습 및 결과물 제작",
                  "현업에 즉시 활용 가능한 고퀄리티 템플릿 제공",
                  "Zoom 라이브 코칭으로 막히는 부분 실시간 해결"
                ].map((item, idx) => (
                  <li key={idx} className="flex items-center gap-3">
                    <CheckCircle className="text-blue-600 flex-shrink-0" size={20} />
                    <span className="text-gray-700 font-medium">{item}</span>
                  </li>
                ))}
              </ul>
            </div>
            <div className="relative h-96 rounded-2xl overflow-hidden shadow-2xl">
              <img 
                src="https://images.unsplash.com/photo-1531482615713-2afd69097998?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" 
                alt="Working on AI project" 
                className="w-full h-full object-cover"
              />
              <div className="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/80 to-transparent p-6">
                <p className="text-white font-bold text-lg">"5주 후, 당신은 전문가(Expert)가 됩니다."</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Curriculum Section */}
      <section id="curriculum" className="py-20 bg-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <span className="text-blue-600 font-bold tracking-wide uppercase">Curriculum</span>
            <h2 className="text-3xl md:text-4xl font-bold text-gray-900 mt-2">
              실무형 AI 전문가가 되는 8가지 열쇠
            </h2>
            <p className="mt-4 text-xl text-gray-500">
              하나하나가 별도의 유료 강의급 가치를 지닌 핵심 과정입니다.
            </p>
          </div>

          <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
            {curriculum.map((item) => (
              <div key={item.id} className="bg-white rounded-2xl p-6 border border-gray-100 shadow-lg hover:shadow-xl transition hover:-translate-y-1 duration-300 group">
                <div className="mb-4 bg-gray-50 rounded-xl p-3 w-fit group-hover:bg-blue-50 transition">
                  {item.icon}
                </div>
                <h3 className="text-xl font-bold text-gray-900 mb-2">{item.title}</h3>
                <p className="text-gray-600 text-sm leading-relaxed">
                  {item.desc}
                </p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Schedule & Info Section */}
      <section id="schedule" className="py-20 bg-slate-900 text-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="bg-gradient-to-r from-blue-900 to-slate-800 rounded-3xl p-8 md:p-12 border border-blue-700/50 shadow-2xl relative overflow-hidden">
            <div className="absolute top-0 right-0 -mt-10 -mr-10 w-40 h-40 bg-blue-500 rounded-full blur-3xl opacity-20"></div>
            
            <div className="grid md:grid-cols-2 gap-12">
              <div>
                <h2 className="text-3xl font-bold mb-8 flex items-center gap-3">
                  <Calendar className="text-blue-400" />
                  교육 일정 및 안내
                </h2>
                
                <div className="space-y-8">
                  <div className="flex gap-4">
                    <div className="w-12 h-12 rounded-full bg-blue-600/20 flex items-center justify-center text-blue-400 font-bold shrink-0">1</div>
                    <div>
                      <h4 className="text-xl font-bold text-blue-100">접수 기간 (5일 한정)</h4>
                      <p className="text-gray-300 mt-1">2026년 1월 26일(월) ~ 1월 30일(금)</p>
                      <p className="text-sm text-red-400 mt-1 font-medium">* 조기 마감될 수 있습니다.</p>
                    </div>
                  </div>
                  
                  <div className="flex gap-4">
                    <div className="w-12 h-12 rounded-full bg-blue-600/20 flex items-center justify-center text-blue-400 font-bold shrink-0">2</div>
                    <div>
                      <h4 className="text-xl font-bold text-blue-100">교육 기간 (5주)</h4>
                      <p className="text-gray-300 mt-1">2026년 2월 11일 ~ 3월 18일</p>
                      <p className="text-sm text-gray-400 mt-1">매주 수요일 저녁 9시 ~ 11시 (2시간)</p>
                    </div>
                  </div>

                  <div className="flex gap-4">
                    <div className="w-12 h-12 rounded-full bg-blue-600/20 flex items-center justify-center text-blue-400 font-bold shrink-0">3</div>
                    <div>
                      <h4 className="text-xl font-bold text-blue-100">교육 방법</h4>
                      <p className="text-gray-300 mt-1 flex items-center gap-2">
                        <Video size={16} /> Zoom / Google Meet 라이브
                      </p>
                      <p className="text-sm text-gray-400 mt-1">이론 30% + 실습 70% 밀착 코칭</p>
                    </div>
                  </div>
                </div>
              </div>

              <div className="bg-white/5 rounded-2xl p-8 border border-white/10 flex flex-col justify-center items-center text-center">
                <AlertCircle className="w-12 h-12 text-yellow-400 mb-4" />
                <h3 className="text-2xl font-bold mb-2">중급자 전용 과정</h3>
                <p className="text-gray-300 mb-6">
                  본 과정은 기초 사용법을 넘어<br/>
                  실질적인 성과 창출을 목표로 합니다.<br/>
                  <span className="text-blue-300">AISH 중급 수료자 또는 이에 준하는 분</span>들만<br/>
                  신청하실 수 있습니다.
                </p>
                <div className="w-full bg-gray-700 h-px mb-6"></div>
                <p className="font-bold text-lg text-white">지금 바로 도전하세요!</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* CTA Form Section */}
      <section id="apply" className="py-20 bg-gray-50">
        <div className="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="bg-white rounded-2xl shadow-xl p-8 md:p-12">
            <div className="text-center mb-10">
              <h2 className="text-3xl font-bold text-gray-900">수강 신청서 작성</h2>
              <p className="text-gray-600 mt-2">
                미래를 바꾸는 5주, 지금 시작됩니다. 정보를 입력해주시면 담당자가 연락드립니다.
              </p>
            </div>

            {showSuccess ? (
              <div className="bg-green-50 border border-green-200 rounded-xl p-8 text-center animate-fade-in">
                <CheckCircle className="w-16 h-16 text-green-500 mx-auto mb-4" />
                <h3 className="text-2xl font-bold text-gray-900 mb-2">신청이 완료되었습니다!</h3>
                <p className="text-gray-600">안내 메일이 곧 발송될 예정입니다. 감사합니다.</p>
              </div>
            ) : (
              <form onSubmit={handleSubmit} className="space-y-6">
                <div>
                  <label htmlFor="name" className="block text-sm font-medium text-gray-700 mb-1">성명</label>
                  <input
                    type="text"
                    id="name"
                    name="name"
                    required
                    className="w-full px-4 py-3 rounded-lg border border-gray-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition outline-none"
                    placeholder="홍길동"
                    value={formData.name}
                    onChange={handleInputChange}
                  />
                </div>

                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label htmlFor="phone" className="block text-sm font-medium text-gray-700 mb-1">연락처</label>
                    <input
                      type="tel"
                      id="phone"
                      name="phone"
                      required
                      className="w-full px-4 py-3 rounded-lg border border-gray-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition outline-none"
                      placeholder="010-1234-5678"
                      value={formData.phone}
                      onChange={handleInputChange}
                    />
                  </div>
                  <div>
                    <label htmlFor="email" className="block text-sm font-medium text-gray-700 mb-1">이메일</label>
                    <input
                      type="email"
                      id="email"
                      name="email"
                      required
                      className="w-full px-4 py-3 rounded-lg border border-gray-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition outline-none"
                      placeholder="example@email.com"
                      value={formData.email}
                      onChange={handleInputChange}
                    />
                  </div>
                </div>

                <div>
                  <label htmlFor="course" className="block text-sm font-medium text-gray-700 mb-1">참가 희망 과정</label>
                  <select
                    id="course"
                    name="course"
                    className="w-full px-4 py-3 rounded-lg border border-gray-300 focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition outline-none"
                    value={formData.course}
                    onChange={handleInputChange}
                  >
                    <option value="all">스페셜 전문가 전체 과정 (8대 핵심 과정)</option>
                    <option value="consulting">상담 후 결정</option>
                  </select>
                </div>

                <div className="pt-4">
                  <button
                    type="submit"
                    className="w-full bg-blue-600 text-white font-bold py-4 rounded-xl text-lg hover:bg-blue-700 transition shadow-lg hover:shadow-xl transform hover:-translate-y-0.5"
                  >
                    전문가 과정 신청 완료하기
                  </button>
                  <p className="text-center text-xs text-gray-400 mt-4">
                    * 제출해주신 정보는 교육 운영 목적 외에는 사용되지 않습니다.
                  </p>
                </div>
              </form>
            )}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-gray-400 py-12 border-t border-gray-800">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="flex flex-col md:flex-row justify-between items-center gap-6">
            <div className="text-center md:text-left">
              <h4 className="text-white text-lg font-bold mb-2">AISH 교육협회</h4>
              <p className="text-sm">AI Smart Work Hub - 업무 혁신을 선도합니다.</p>
              <p className="text-sm mt-1">문의: admin@aish.kr | 02-123-4567</p>
            </div>
            <div className="flex space-x-6">
              <a href="#" className="hover:text-white transition"><Youtube size={24} /></a>
              <a href="#" className="hover:text-white transition"><div className="w-6 h-6 bg-green-500 rounded text-black font-bold text-xs flex items-center justify-center">N</div></a>
            </div>
          </div>
          <div className="mt-8 pt-8 border-t border-gray-800 text-center text-xs">
            &copy; 2026 AISH Education Association. All rights reserved.
          </div>
        </div>
      </footer>
    </div>
  );
};

export default AishLandingPage;
