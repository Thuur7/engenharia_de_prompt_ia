import { useEffect, useState, useCallback, useRef } from 'react';

interface TranslatorState {
  sourceText: string;
  translatedText: string;
  isLoading: boolean;
  error: string | null;
  characterCount: number;
}

const STORAGE_KEY = 'translator_source_text';
const DEBOUNCE_DELAY = 300; // 300ms

// Função para fazer a tradução via API
async function translateText(text: string): Promise<string> {
  if (!text.trim()) return '';

  try {
    const response = await fetch(
      `https://api.mymemory.translated.net/get?q=${encodeURIComponent(text )}&langpair=en|pt-BR`,
      { method: 'GET' }
    );

    if (!response.ok) throw new Error('Erro na tradução');

    const data = await response.json();

    if (data.responseStatus === 200) {
      return data.responseData.translatedText;
    } else if (data.responseStatus === 429) {
      throw new Error('Muitas requisições. Aguarde um momento.');
    } else {
      throw new Error('Erro ao traduzir texto');
    }
  } catch (error) {
    throw new Error(
      error instanceof Error ? error.message : 'Erro desconhecido na tradução'
    );
  }
}

// Hook principal
export function useTranslator() {
  // ESTADOS
  const [sourceText, setSourceTextState] = useState('');
  const [translatedText, setTranslatedText] = useState('');
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState<string | null>(null);

  // REFS
  const debounceTimerRef = useRef<NodeJS.Timeout | null>(null);

  // EFEITO: Executar quando sourceText muda
  useEffect(() => {
    // Limpar timer anterior
    if (debounceTimerRef.current) {
      clearTimeout(debounceTimerRef.current);
    }

    // Se texto está vazio, limpar tudo
    if (!sourceText.trim()) {
      setTranslatedText('');
      setError(null);
      setIsLoading(false);
      return;
    }

    // Mostrar que está carregando
    setIsLoading(true);
    setError(null);

    // DEBOUNCE: Aguardar 300ms antes de traduzir
    debounceTimerRef.current = setTimeout(async () => {
      try {
        const translated = await translateText(sourceText);
        setTranslatedText(translated);
        setIsLoading(false);
        setError(null);
      } catch (error) {
        setIsLoading(false);
        setError(error instanceof Error ? error.message : 'Erro desconhecido');
      }
    }, DEBOUNCE_DELAY);

    // CLEANUP
    return () => {
      if (debounceTimerRef.current) {
        clearTimeout(debounceTimerRef.current);
      }
    };
  }, [sourceText]);

  // FUNÇÕES
  const setSourceText = useCallback((text: string) => {
    setSourceTextState(text);
    localStorage.setItem(STORAGE_KEY, text);
  }, []);

  const clearAll = useCallback(() => {
    setSourceTextState('');
    setTranslatedText('');
    setIsLoading(false);
    setError(null);
    localStorage.removeItem(STORAGE_KEY);
  }, []);

  const swapLanguages = useCallback(() => {
    setSourceTextState(translatedText);
    setTranslatedText('');
    setIsLoading(false);
    setError(null);
    localStorage.setItem(STORAGE_KEY, translatedText);
  }, [translatedText]);

  const copyTranslation = useCallback(async () => {
    try {
      await navigator.clipboard.writeText(translatedText);
      return true;
    } catch {
      return false;
    }
  }, [translatedText]);

  // RETORNAR
  return {
    sourceText,
    translatedText,
    isLoading,
    error,
    characterCount: sourceText.length,
    setSourceText,
    clearAll,
    swapLanguages,
    copyTranslation,
  };
}

import { useState } from 'react';
import { useTheme } from '@/contexts/ThemeContext';
import { useTranslator } from '@/hooks/useTranslator';
import {
  Copy,
  Trash2,
  ArrowRightLeft,
  Moon,
  Sun,
} from 'lucide-react';
import { toast } from 'sonner';

export default function Home() {
  const {
    sourceText,
    translatedText,
    isLoading,
    error,
    characterCount,
    setSourceText,
    clearAll,
    swapLanguages,
    copyTranslation,
  } = useTranslator();

  const { theme, toggleTheme } = useTheme();
  const [copiedRecently, setCopiedRecently] = useState(false);

  const handleCopyTranslation = async () => {
    const success = await copyTranslation();
    if (success) {
      setCopiedRecently(true);
      toast.success('Tradução copiada para a área de transferência!');
      setTimeout(() => setCopiedRecently(false), 2000);
    } else {
      toast.error('Erro ao copiar tradução');
    }
  };

  const handleClearAll = () => {
    clearAll();
    toast.info('Texto limpo');
  };

  const handleSwapLanguages = () => {
    swapLanguages();
    toast.info('Idiomas invertidos');
  };

  return (
    <div className="min-h-screen bg-background text-foreground">
      {/* HEADER */}
      <header className="border-b border-border bg-card shadow-sm">
        <div className="mx-auto flex max-w-7xl items-center justify-between px-4 py-6">
          <div>
            <h1 className="text-3xl font-bold">Translator</h1>
            <p className="text-sm text-muted-foreground">
              Tradução instantânea de inglês para português
            </p>
          </div>

          <button
            onClick={toggleTheme}
            className="h-10 w-10 p-0 rounded-lg hover:bg-secondary"
            aria-label="Alternar tema"
          >
            {theme === 'light' ? (
              <Moon className="h-5 w-5" />
            ) : (
              <Sun className="h-5 w-5" />
            )}
          </button>
        </div>
      </header>

      {/* MAIN */}
      <main className="mx-auto max-w-7xl px-4 py-8">
        <div className="grid gap-8 lg:grid-cols-2">
          {/* PAINEL ESQUERDO */}
          <div className="flex flex-col gap-4">
            <div className="flex items-center justify-between">
              <label className="text-sm font-medium">Inglês</label>
              <span className="text-xs text-muted-foreground">
                {characterCount} caracteres
              </span>
            </div>

            <textarea
              value={sourceText}
              onChange={(e) => setSourceText(e.target.value)}
              placeholder="Digite o texto em inglês aqui..."
              className="w-full rounded-lg border border-input px-4 py-3 min-h-64 resize-none focus:border-primary focus:ring-2 focus:ring-primary/20"
              spellCheck="true"
            />

            <div className="flex gap-2">
              <button
                onClick={handleClearAll}
                className="flex items-center gap-2 px-4 py-2 rounded-lg bg-secondary hover:bg-secondary/80 transition-colors"
              >
                <Trash2 className="h-4 w-4" />
                Limpar
              </button>
              <button
                onClick={handleSwapLanguages}
                className="flex items-center gap-2 px-4 py-2 rounded-lg bg-secondary hover:bg-secondary/80 transition-colors"
              >
                <ArrowRightLeft className="h-4 w-4" />
                Inverter
              </button>
            </div>
          </div>

          {/* PAINEL DIREITO */}
          <div className="flex flex-col gap-4">
            <div className="flex items-center justify-between">
              <label className="text-sm font-medium">Português (Brasil)</label>
              <span className="text-xs text-muted-foreground">
                {translatedText.length} caracteres
              </span>
            </div>

            <div className="rounded-lg border border-border bg-card p-4 min-h-64">
              {isLoading ? (
                <div className="flex items-center gap-2 text-primary">
                  <div className="animate-spin rounded-full border-2 border-current border-t-transparent h-4 w-4" />
                  <span>Traduzindo...</span>
                </div>
              ) : error ? (
                <div className="text-red-500">
                  <p className="font-medium">Erro na tradução</p>
                  <p className="text-sm">{error}</p>
                </div>
              ) : translatedText ? (
                <p className="whitespace-pre-wrap">{translatedText}</p>
              ) : (
                <p className="text-muted-foreground">
                  A tradução aparecerá aqui automaticamente
                </p>
              )}
            </div>

            {translatedText && !isLoading && !error && (
              <button
                onClick={handleCopyTranslation}
                className="flex items-center gap-2 px-4 py-2 rounded-lg bg-primary text-primary-foreground hover:bg-primary/90 transition-colors"
              >
                <Copy className="h-4 w-4" />
                {copiedRecently ? 'Copiado!' : 'Copiar'}
              </button>
            )}
          </div>
        </div>
      </main>

      {/* FOOTER */}
      <footer className="border-t border-border bg-card py-6 text-center text-xs text-muted-foreground">
        <p>© 2026 Translator App</p>
      </footer>
    </div>
  );
}

import { createContext, useContext, useEffect, useState } from 'react';

const ThemeContext = createContext<{
  theme: 'light' | 'dark';
  toggleTheme: () => void;
} | undefined>(undefined);

export function ThemeProvider({
  children,
  defaultTheme = 'light',
  switchable = false,
}: {
  children: React.ReactNode;
  defaultTheme?: 'light' | 'dark';
  switchable?: boolean;
}) {
  const [theme, setTheme] = useState<'light' | 'dark'>(defaultTheme);

  useEffect(() => {
    const html = document.documentElement;
    if (theme === 'dark') {
      html.classList.add('dark');
    } else {
      html.classList.remove('dark');
    }
  }, [theme]);

  const toggleTheme = () => {
    setTheme((prev) => (prev === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export function useTheme() {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme deve ser usado dentro de ThemeProvider');
  }
  return context;
}

@import "tailwindcss";

:root {
  --primary: oklch(0.5 0.15 250);        /* Azul profundo */
  --primary-foreground: oklch(0.99 0 0); /* Branco */
  --secondary: oklch(0.95 0.01 0);       /* Cinza claro */
  --secondary-foreground: oklch(0.2 0.01 0); /* Cinza escuro */
  --accent: oklch(0.7 0.12 140);         /* Verde suave */
  --background: oklch(0.99 0.001 0);     /* Branco */
  --foreground: oklch(0.2 0.01 0);       /* Cinza escuro */
  --card: oklch(0.99 0.001 0);           /* Branco */
  --card-foreground: oklch(0.2 0.01 0);  /* Cinza escuro */
  --border: oklch(0.93 0.002 0);         /* Cinza muito claro */
  --input: oklch(0.93 0.002 0);          /* Cinza muito claro */
  --muted: oklch(0.95 0.01 0);           /* Cinza claro */
  --muted-foreground: oklch(0.5 0.01 0); /* Cinza médio */
}

.dark {
  --primary: oklch(0.65 0.12 250);       /* Azul mais claro */
  --background: oklch(0.15 0.01 0);      /* Cinza muito escuro */
  --foreground: oklch(0.92 0.005 0);     /* Branco */
  --card: oklch(0.21 0.006 286);         /* Cinza escuro */
  --card-foreground: oklch(0.92 0.005 0); /* Branco */
  --border: oklch(0.3 0.01 0);           /* Cinza escuro */
  --input: oklch(0.3 0.01 0);            /* Cinza escuro */
  --secondary: oklch(0.25 0.01 0);       /* Cinza escuro */
  --muted: oklch(0.4 0.01 0);            /* Cinza médio */
  --muted-foreground: oklch(0.7 0.01 0); /* Cinza claro */
}

@layer base {
  body {
    @apply bg-background text-foreground;
    font-family: 'Inter', sans-serif;
  }

  h1, h2, h3, h4, h5, h6 {
    font-family: 'Geist', sans-serif;
    font-weight: 700;
  }
}

@layer components {
  .translator-input {
    @apply w-full rounded-lg border border-input px-4 py-3 
           focus:border-primary focus:ring-2 focus:ring-primary/20
           transition-all duration-200;
  }

  .translator-button {
    @apply px-4 py-2 rounded-lg font-medium transition-all duration-200
           hover:scale-105 active:scale-95;
  }

  .translator-button-primary {
    @apply bg-primary text-primary-foreground hover:bg-primary/90;
  }

  .translator-button-secondary {
    @apply bg-secondary text-secondary-foreground hover:bg-secondary/80;

  }
}

import { Toaster } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";
import NotFound from "@/pages/NotFound";
import { Route, Switch } from "wouter";
import ErrorBoundary from "./components/ErrorBoundary";
import { ThemeProvider } from "./contexts/ThemeContext";
import Home from "./pages/Home";

function Router() {
  return (
    <Switch>
      <Route path={"/"} component={Home} />
      <Route path={"/404"} component={NotFound} />
      <Route component={NotFound} />
    </Switch>
  );
}

function App() {
  return (
    <ErrorBoundary>
      <ThemeProvider defaultTheme="light" switchable>
        <TooltipProvider>
          <Toaster />
          <Router />
        </TooltipProvider>
      </ThemeProvider>
    </ErrorBoundary>
  );
}

export default App;
