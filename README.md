{
  "name": "diyas-portfolio",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "framer-motion": "^11.0.0",
    "lucide-react": "^0.300.0",
    "next": "14.1.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/node": "^20.11.0",
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "autoprefixer": "^10.4.17",
    "postcss": "^8.4.35",
    "tailwindcss": "^3.4.1",
    "typescript": "^5.3.3"
  }
}
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import "./globals.css";

const inter = Inter({ subsets: ["latin"] });

export const metadata: Metadata = {
  title: "Diya Tomar | Creative Developer",
  description: "B.Tech Computer Science Student & Frontend Developer Portfolio",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  Buffer
  return (
    <html lang="en" className="scroll-smooth">
      <body className={`${inter.className} bg-[#0A0A0C] text-white antialiased`}>
        {children}
      </body>
    </html>
  );
}
'use client';

import Navigation from '@/components/navigation';
import Hero from '@/components/hero';
import About from '@/components/about';
import Skills from '@/components/skills';
import Projects from '@/components/projects';
import Contact from '@/components/contact';
import Footer from '@/components/footer';

export default function Home() {
  return (
    <main className="min-h-screen bg-[#0A0A0C]">
      <Navigation />
      <Hero />
      <About />
      <Skills />
      <Projects />
      <Contact />
      <Footer />
    </main>
  );
}
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --background: #0A0A0C;
  --foreground: #FFFFFF;
}

body {
  background-color: var(--background);
  color: var(--foreground);
  overflow-x: hidden;
}

/* Custom smooth animation timing function like Apple */
.cubic-bezier-apple {
  transition-timing-function: cubic-bezier(0.25, 0.1, 0, 1);
}
'use client';

import { useState, useEffect } from 'react';
import { Menu, X } from 'lucide-react';

export default function Navigation() {
  const [isOpen, setIsOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 50);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    <nav className={`fixed top-0 w-full z-50 transition-all duration-500 ${scrolled ? 'bg-[#0A0A0C]/70 backdrop-blur-xl border-b border-white/5' : 'bg-transparent'}`}>
      <div className="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
        <a href="#" className="text-xl font-medium tracking-tight hover:opacity-70 transition-opacity">
          diya tomar
        </a>
        
        <div className="hidden md:flex items-center gap-8 text-sm font-light text-white/60">
          <a href="#about" className="hover:text-white transition-colors">About</a>
          <a href="#skills" className="hover:text-white transition-colors">Skills</a>
          <a href="#projects" className="hover:text-white transition-colors">Projects</a>
          <a href="#contact" className="hover:text-white transition-colors">Contact</a>
        </div>

        <button onClick={() => setIsOpen(!isOpen)} className="md:hidden text-white">
          {isOpen ? <X size={24} /> : <Menu size={24} />}
        </button>
      </div>

      {/* Mobile Menu */}
      {isOpen && (
        <div className="md:hidden fixed inset-0 top-20 bg-[#0A0A0C] z-40 flex flex-col p-6 gap-6 text-2xl font-light border-t border-white/5 animate-fade-in">
          <a href="#about" onClick={() => setIsOpen(false)}>About</a>
          <a href="#skills" onClick={() => setIsOpen(false)}>Skills</a>
          <a href="#projects" onClick={() => setIsOpen(false)}>Projects</a>
          <a href="#contact" onClick={() => setIsOpen(false)}>Contact</a>
        </div>
      )}
    </nav>
  );
}
'use client';

import { motion } from 'framer-motion';

export default function Hero() {
  return (
    <section className="min-h-screen flex flex-col justify-center items-center px-6 pt-20 text-center relative overflow-hidden">
      <motion.div 
        initial={{ opacity: 0, y: 40 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 1, ease: [0.25, 0.1, 0, 1] }}
        className="space-y-6 max-w-4xl"
      >
        <span className="inline-block px-4 py-1.5 rounded-full bg-white/5 border border-white/10 text-xs tracking-wide text-white/80 backdrop-blur-md">
          ✨ Coding my way up
        </span>
        
        <h1 className="text-5xl md:text-8xl font-bold tracking-tight text-white leading-none">
          Hi, I'm <span className="bg-gradient-to-r from-pink-500 via-purple-500 to-indigo-500 bg-clip-text text-transparent">Diya Tomar</span>
        </h1>
        
        <p className="text-xl md:text-2xl text-white/40 font-light max-w-2xl mx-auto">
          B.Tech Computer Science Student | Frontend Developer (Beginner)
        </p>

        <div className="pt-8 flex flex-col sm:flex-row justify-center gap-4">
          <a href="#projects" className="px-8 py-4 rounded-full bg-white text-black font-medium text-sm hover:bg-white/90 transition-colors">
            View Projects
          </a>
          <a href="#contact" className="px-8 py-4 rounded-full bg-white/5 border border-white/10 text-white font-medium text-sm hover:bg-white/10 transition-colors backdrop-blur-md">
            Get in Touch
          </a>
        </div>
      </motion.div>
      
      <div className="absolute bottom-10 left-1/2 -translate-x-1/2 text-xs tracking-widest text-white/20 animate-bounce">
        SCROLL
      </div>
    </section>
  );
}
'use client';

import { motion } from 'framer-motion';

export default function About() {
  return (
    <section id="about" className="py-32 md:py-48 max-w-5xl mx-auto px-6">
      <div className="grid md:grid-cols-12 gap-12 items-center">
        <div className="md:col-span-4">
          <p className="text-xs font-semibold tracking-widest text-white/40 uppercase mb-3">About Me</p>
          <h2 className="text-4xl font-bold tracking-tight">Turning coffee into cute, functional frontends. ✨</h2>
        </div>
        <div className="md:col-span-8 space-y-6 text-lg text-white/60 font-light leading-relaxed">
          <p>
            I'm a B.Tech Computer Science student at <strong>Galgotias University</strong> with a keen interest in frontend development and building clean, beautiful web experiences.
          </p>
          <p>
            As a girl navigating the tech space, I thrive on crafting highly visual, interactive, and seamless digital creations. I like keeping my code neat and my style minimal. Currently experimenting with modern web tools like React and Tailwind CSS.
          </p>
          <div className="pt-4 flex flex-wrap gap-4 text-sm text-white/40">
            <span className="px-4 py-2 bg-white/5 rounded-2xl border border-white/5">📍 Greater Noida, UP, India</span>
            <span className="px-4 py-2 bg-white/5 rounded-2xl border border-white/5">🎓 Galgotias University (B.Tech CSE)</span>
          </div>
        </div>
      </div>
    </section>
  );
}
'use client';

const skills = [
  { name: "HTML5 / CSS3", category: "Frontend" },
  { name: "JavaScript (ES6+)", category: "Frontend" },
  { name: "React.js", category: "Frontend" },
  { name: "Tailwind CSS", category: "Frontend" },
  { name: "Next.js (Learning)", category: "Frontend" },
  { name: "Git / GitHub", category: "Tools" }
];

export default function Skills() {
  return (
    <section id="skills" className="py-32 md:py-48 max-w-5xl mx-auto px-6 border-t border-white/5">
      <p className="text-xs font-semibold tracking-widest text-white/40 uppercase mb-3">Skills</p>
      <h2 className="text-4xl font-bold tracking-tight mb-16">My Tech Stack</h2>
      
      <div className="grid sm:grid-cols-2 md:grid-cols-3 gap-6">
        {skills.map((skill, index) => (
          <div key={index} className="p-6 rounded-3xl bg-white/[0.02] border border-white/5 hover:border-white/10 transition-colors">
            <span className="text-xs font-mono text-white/30 uppercase block mb-2">{skill.category}</span>
            <h3 className="text-xl font-medium tracking-tight">{skill.name}</h3>
          </div>
        ))}
      </div>
    </section>
  );
}
'use client';

const projects = [
  {
    title: "Personal Portfolio",
    description: "A premium, Apple-inspired minimal portfolio website built using Next.js and Tailwind CSS.",
    tags: ["React", "Next.js", "Tailwind CSS"]
  },
  {
    title: "E-Commerce Frontend",
    description: "A clean and responsive shopping website landing page with modern interactive UI components.",
    tags: ["HTML", "CSS", "JavaScript"]
  }
];

export default function Projects() {
  return (
    <section id="projects" className="py-32 md:py-48 max-w-5xl mx-auto px-6 border-t border-white/5">
      <p className="text-xs font-semibold tracking-widest text-white/40 uppercase mb-3">Work</p>
      <h2 className="text-4xl font-bold tracking-tight mb-16">Featured Projects</h2>

      <div className="grid md:grid-cols-2 gap-8">
        {projects.map((project, index) => (
          <div key={index} className="group relative p-8 rounded-3xl bg-white/[0.02] border border-white/5 overflow-hidden hover:bg-white/[0.04] transition-all duration-500">
            <h3 className="text-2xl font-bold tracking-tight mb-2">{project.title}</h3>
            <p className="text-white/50 font-light mb-6 leading-relaxed">{project.description}</p>
            <div className="flex flex-wrap gap-2">
              {project.tags.map((tag, idx) => (
                <span key={idx} className="text-xs px-3 py-1 bg-white/5 rounded-full border border-white/5 text-white/60">{tag}</span>
              ))}
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}
'use client';

export default function Contact() {
  return (
    <section id="contact" className="py-32 md:py-48 max-w-5xl mx-auto px-6 border-t border-white/5 text-center">
      <p className="text-xs font-semibold tracking-widest text-white/40 uppercase mb-3">Connect</p>
      <h2 className="text-5xl md:text-7xl font-bold tracking-tight mb-6">Let's work together.</h2>
      <p className="text-white/50 font-light max-w-md mx-auto mb-10 leading-relaxed">
        I'm currently looking for frontend projects and internship opportunities. Feel free to reach out!
      </p>
      <a href="mailto:your-email@example.com" className="inline-block px-8 py-4 rounded-full bg-white text-black font-medium text-sm hover:bg-white/90 transition-colors">
        Get In Touch
      </a>
    </section>
  );
}
'use client';

export default function Footer() {
  return (
    <footer className="py-12 border-t border-white/5 text-center text-xs text-white/30 font-light">
      <div className="max-w-5xl mx-auto px-6 flex flex-col sm:flex-row items-center justify-between gap-4">
        <span className="font-medium text-white/50">diya tomar</span>
        <p>© 2026 Diya Tomar. All rights reserved.</p>
        <span>Made in Bolt</span>
      </div>
    </footer>
  );
}
