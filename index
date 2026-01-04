import React, { useEffect, useRef, useState } from 'react';
import { CupSoda, Candy, Coffee, Cookie, Star, Users, CheckCircle, Flame, Droplets, Gift, Clock, Download, Handshake } from 'lucide-react';

const RewardTier = ({ tokens, items, color, icon: Icon }) => {
  return (
    <div className={`flex flex-col h-full rounded-2xl border-2 overflow-hidden transition-all hover:shadow-lg ${color.border} ${color.bg}`}>
      <div className={`p-4 flex items-center justify-between ${color.headerBg} text-white`}>
        <div className="flex items-center gap-2">
          <Icon size={24} />
          <h2 className="text-xl font-bold uppercase tracking-wider">{tokens} {tokens === 1 ? 'Token' : 'Tokens'}</h2>
        </div>
      </div>
      <div className="p-5 flex-grow">
        <ul className="space-y-3">
          {items.map((item, index) => (
            <li key={index} className="flex items-start gap-2 text-gray-700 text-sm md:text-base">
              <span className={`mt-1.5 h-2 w-2 rounded-full shrink-0 ${color.dot}`} />
              <span className="font-medium">{item}</span>
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
};

const App = () => {
  const chartRef = useRef(null);
  const [isDownloading, setIsDownloading] = useState(false);

  // Load html2canvas from CDN
  useEffect(() => {
    const script = document.createElement('script');
    script.src = "https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js";
    script.async = true;
    document.body.appendChild(script);
    return () => {
      document.body.removeChild(script);
    };
  }, []);

  const handleDownload = async () => {
    if (!window.html2canvas) {
      alert("Still loading image engine. Please try again in a second!");
      return;
    }

    setIsDownloading(true);
    try {
      const canvas = await window.html2canvas(chartRef.current, {
        scale: 2, // Higher quality
        useCORS: true,
        backgroundColor: '#f8fafc' // Matches slate-50
      });
      
      const image = canvas.toDataURL("image/png");
      const link = document.createElement('a');
      link.href = image;
      link.download = "Werkheiser-Reward-Chart.png";
      link.click();
    } catch (err) {
      console.error("Download failed", err);
    } finally {
      setIsDownloading(false);
    }
  };

  const tiers = [
    {
      tokens: 1,
      icon: Candy,
      color: {
        border: 'border-blue-100',
        bg: 'bg-blue-50/30',
        headerBg: 'bg-blue-600',
        dot: 'bg-blue-500'
      },
      items: ['Fruit Snack', 'Mini Water', 'Piece of Candy']
    },
    {
      tokens: 2,
      icon: Coffee,
      color: {
        border: 'border-orange-100',
        bg: 'bg-orange-50/30',
        headerBg: 'bg-orange-500',
        dot: 'bg-orange-500'
      },
      items: [
        'Coffee',
        'Hot Chocolate',
        'Cappuccino',
        'Tea (Coming Soon)',
        'Chips (Variety Pack)',
        'Cheez-Its',
        'Takis',
        'Doritos'
      ]
    },
    {
      tokens: 3,
      icon: Cookie,
      color: {
        border: 'border-emerald-100',
        bg: 'bg-emerald-50/30',
        headerBg: 'bg-emerald-600',
        dot: 'bg-emerald-500'
      },
      items: ['Nutrigrain Bar', 'Rice Krispie Treat', 'Pringles']
    },
    {
      tokens: 5,
      icon: Star,
      color: {
        border: 'border-purple-100',
        bg: 'bg-purple-50/30',
        headerBg: 'bg-purple-600',
        dot: 'bg-purple-500'
      },
      items: [
        'Classwork Assignment Excused',
        '5 Bonus Points (Larger Assignment)'
      ]
    },
    {
      tokens: 10,
      icon: Gift,
      color: {
        border: 'border-rose-100',
        bg: 'bg-rose-50/30',
        headerBg: 'bg-rose-600',
        dot: 'bg-rose-500'
      },
      items: ['Full Brownie Tray']
    },
    {
      tokens: 50,
      icon: Users,
      color: {
        border: 'border-yellow-200',
        bg: 'bg-yellow-50/40',
        headerBg: 'bg-yellow-600',
        dot: 'bg-yellow-600'
      },
      items: [
        'WHOLE CLASS: Free Day',
        'WHOLE CLASS: Brownie Party'
      ]
    }
  ];

  return (
    <div className="min-h-screen bg-slate-100 py-6 px-4 sm:px-6 lg:px-8 font-sans">
      <div className="max-w-6xl mx-auto">
        {/* Control Panel (Not included in image) */}
        <div className="flex justify-end mb-6 no-print">
          <button
            onClick={handleDownload}
            disabled={isDownloading}
            className="flex items-center gap-2 bg-slate-800 hover:bg-slate-900 text-white px-5 py-2.5 rounded-full font-bold transition-all shadow-md active:scale-95 disabled:opacity-50"
          >
            <Download size={18} />
            {isDownloading ? 'Generating...' : 'Download as Image'}
          </button>
        </div>

        {/* The Capture Area */}
        <div ref={chartRef} className="bg-slate-50 p-8 rounded-3xl shadow-sm border border-slate-200">
          <header className="text-center mb-10">
            <div className="inline-flex items-center justify-center p-3 bg-yellow-100 rounded-full mb-4 shadow-sm">
              <Flame className="text-yellow-600" size={40} />
            </div>
            <h1 className="text-4xl md:text-5xl font-black text-slate-800 tracking-tight mb-2">
              WERKHEISER REWARDS
            </h1>
            <p className="text-slate-600 text-lg font-medium max-w-2xl mx-auto">
              Redeem your tokens for snacks, perks, and class-wide celebrations!
            </p>
          </header>

          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-8">
            {tiers.map((tier) => (
              <RewardTier key={tier.tokens} {...tier} />
            ))}
          </div>

          <footer className="mt-12 text-center border-t border-slate-200 pt-8">
            <div className="flex flex-col items-center gap-4">
              <div className="flex flex-wrap justify-center gap-6">
                <div className="flex items-center gap-2 text-slate-500">
                  <Clock size={18} />
                  <p className="text-sm font-semibold uppercase tracking-widest text-left">Redemption: <span className="font-normal capitalize tracking-normal italic block">See Mr. Werkheiser before/after class</span></p>
                </div>
                <div className="flex items-center gap-2 text-blue-600 bg-blue-50 px-4 py-2 rounded-full border border-blue-100 shadow-sm">
                  <Handshake size={20} />
                  <p className="text-sm font-bold uppercase tracking-tight">Tokens are Transferable & Combinable!</p>
                </div>
              </div>
              <p className="text-slate-400 text-xs italic">
                Work together with your classmates to reach the high-tier rewards!
              </p>
            </div>
          </footer>
        </div>
      </div>
      
      {/* Basic responsive style for print and capture */}
      <style>{`
        @media print {
          .no-print { display: none !important; }
        }
      `}</style>
    </div>
  );
};

export default App;

