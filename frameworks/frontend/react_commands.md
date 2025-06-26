# React Commands

React es una biblioteca de JavaScript para construir interfaces de usuario, especialmente aplicaciones web de una sola página donde necesitas un manejo rápido e interactivo de datos.

## Instalación

### Crear nueva aplicación React
```bash
npx create-react-app my-app
cd my-app
```

### Crear aplicación con TypeScript
```bash
npx create-react-app my-app --template typescript
```

### Crear aplicación con template específico
```bash
npx create-react-app my-app --template redux
npx create-react-app my-app --template redux-typescript
```

### Instalar React en proyecto existente
```bash
npm install react react-dom
npm install --save-dev @types/react @types/react-dom  # Para TypeScript
```

## Comandos de Desarrollo

### Iniciar servidor de desarrollo
```bash
npm start
```

### Ejecutar en puerto específico
```bash
PORT=3001 npm start
```

### Ejecutar con HTTPS
```bash
HTTPS=true npm start
```

### Construir para producción
```bash
npm run build
```

### Ejecutar tests
```bash
npm test
```

### Ejecutar tests sin watch mode
```bash
CI=true npm test
```

### Ejecutar tests con coverage
```bash
npm test -- --coverage
```

### Eject (exponer configuración)
```bash
npm run eject
```

## Comandos con Vite (alternativa moderna)

### Crear proyecto React con Vite
```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
```

### Con TypeScript
```bash
npm create vite@latest my-react-app -- --template react-ts
```

### Ejecutar desarrollo con Vite
```bash
npm run dev
```

### Construir con Vite
```bash
npm run build
```

### Preview de build
```bash
npm run preview
```

## Herramientas de Desarrollo

### Instalar React Developer Tools (extensión del navegador)
Disponible para Chrome y Firefox

### Instalar Storybook
```bash
npx storybook@latest init
```

### Ejecutar Storybook
```bash
npm run storybook
```

### Construir Storybook
```bash
npm run build-storybook
```

## Librerías Populares de React

### React Router (enrutamiento)
```bash
npm install react-router-dom
npm install --save-dev @types/react-router-dom  # Para TypeScript
```

### Redux (gestión de estado)
```bash
npm install @reduxjs/toolkit react-redux
npm install --save-dev @types/react-redux  # Para TypeScript
```

### Material-UI (componentes UI)
```bash
npm install @mui/material @emotion/react @emotion/styled
```

### Styled Components
```bash
npm install styled-components
npm install --save-dev @types/styled-components  # Para TypeScript
```

### Formik (formularios)
```bash
npm install formik yup
```

### React Hook Form
```bash
npm install react-hook-form
```

### Axios (cliente HTTP)
```bash
npm install axios
```

### React Query (gestión de estado del servidor)
```bash
npm install @tanstack/react-query
```

### Zustand (gestión de estado)
```bash
npm install zustand
```

## Testing

### Instalar Testing Library adicional
```bash
npm install --save-dev @testing-library/user-event
npm install --save-dev @testing-library/jest-dom
```

### Instalar Enzyme (alternativa)
```bash
npm install --save-dev enzyme @wojtekmaj/enzyme-adapter-react-17
```

### Ejecutar tests específicos
```bash
npm test -- --testNamePattern="MyComponent"
```

### Ejecutar tests de un archivo
```bash
npm test -- MyComponent.test.js
```

## Linting y Formateo

### Instalar ESLint
```bash
npm install --save-dev eslint eslint-plugin-react
npx eslint --init
```

### Ejecutar ESLint
```bash
npx eslint src/
```

### Instalar Prettier
```bash
npm install --save-dev prettier
```

### Formatear código
```bash
npx prettier --write src/
```

### Instalar Husky para pre-commit hooks
```bash
npm install --save-dev husky lint-staged
npx husky install
```

## Deployment

### Construir para producción
```bash
npm run build
```

### Servir build localmente
```bash
npm install -g serve
serve -s build
```

### Deploy a Netlify
```bash
npm install -g netlify-cli
netlify deploy --prod --dir=build
```

### Deploy a Vercel
```bash
npm install -g vercel
vercel --prod
```

### Deploy a GitHub Pages
```bash
npm install --save-dev gh-pages
```

### Agregar script de deploy
```json
{
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d build"
  }
}
```

## Optimización

### Analizar bundle
```bash
npm install --save-dev webpack-bundle-analyzer
npm run build
npx webpack-bundle-analyzer build/static/js/*.js
```

### Con Vite Bundle Analyzer
```bash
npm install --save-dev rollup-plugin-visualizer
```

### Code splitting automático
React ya incluye code splitting con `React.lazy()`

### Memoización
Usar `React.memo()`, `useMemo()`, `useCallback()`

## React Native (móvil)

### Instalar React Native CLI
```bash
npm install -g @react-native-community/cli
```

### Crear proyecto React Native
```bash
npx react-native init MyApp
```

### Ejecutar en iOS
```bash
npx react-native run-ios
```

### Ejecutar en Android
```bash
npx react-native run-android
```

### Con Expo
```bash
npm install -g @expo/cli
npx create-expo-app MyApp
cd MyApp
npx expo start
```

## Next.js (React con SSR)

### Crear aplicación Next.js
```bash
npx create-next-app@latest my-app
cd my-app
```

### Con TypeScript
```bash
npx create-next-app@latest my-app --typescript
```

### Ejecutar desarrollo
```bash
npm run dev
```

### Construir para producción
```bash
npm run build
```

### Iniciar en producción
```bash
npm start
```

## Herramientas de Build Alternativas

### Parcel
```bash
npm install -g parcel-bundler
parcel index.html
```

### Webpack (manual)
```bash
npm install --save-dev webpack webpack-cli webpack-dev-server
```

### Rollup
```bash
npm install --save-dev rollup
```

## Debugging

### React DevTools Profiler
Usar la pestaña "Profiler" en React DevTools

### Source maps en desarrollo
Habilitado por defecto en Create React App

### Debug en VSCode
Configurar `.vscode/launch.json` para debugging

## Comandos Útiles de Package.json

### Scripts típicos para React
```json
{
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "format": "prettier --write src/"
  }
}
```

## Actualización de Dependencias

### Verificar dependencias desactualizadas
```bash
npm outdated
```

### Actualizar React
```bash
npm update react react-dom
```

### Actualizar Create React App
```bash
npm install react-scripts@latest
```

## Micro-frontends

### Module Federation (Webpack 5)
```bash
npm install --save-dev @module-federation/webpack
```

### Single-SPA
```bash
npm install single-spa
```

## React AI/ML Integration

### React with TensorFlow.js

#### Setup TensorFlow.js in React
```bash
# Instalar TensorFlow.js para React
npm install @tensorflow/tfjs @tensorflow/tfjs-vis

# Para modelos preentrenados
npm install @tensorflow-models/mobilenet
npm install @tensorflow-models/coco-ssd
npm install @tensorflow-models/toxicity
npm install @tensorflow-models/universal-sentence-encoder

# Crear componente de clasificación de imágenes
cat > src/components/ImageClassifier.js << 'EOF'
import React, { useState, useRef, useEffect } from 'react';
import * as tf from '@tensorflow/tfjs';
import * as mobilenet from '@tensorflow-models/mobilenet';

const ImageClassifier = () => {
  const [model, setModel] = useState(null);
  const [imageURL, setImageURL] = useState('');
  const [results, setResults] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const fileInputRef = useRef();

  useEffect(() => {
    const loadModel = async () => {
      console.log('Loading MobileNet model...');
      const loadedModel = await mobilenet.load();
      setModel(loadedModel);
      console.log('Model loaded successfully');
    };
    loadModel();
  }, []);

  const classifyImage = async (imageElement) => {
    if (model) {
      setIsLoading(true);
      try {
        const predictions = await model.classify(imageElement);
        setResults(predictions);
      } catch (error) {
        console.error('Classification error:', error);
      }
      setIsLoading(false);
    }
  };

  const handleImageUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        setImageURL(e.target.result);
        
        const img = new Image();
        img.onload = () => classifyImage(img);
        img.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }
  };

  return (
    <div style={{ padding: '20px', maxWidth: '600px', margin: '0 auto' }}>
      <h2>AI Image Classifier</h2>
      
      <input
        type="file"
        accept="image/*"
        onChange={handleImageUpload}
        ref={fileInputRef}
        style={{ marginBottom: '20px' }}
      />
      
      {imageURL && (
        <div style={{ marginBottom: '20px' }}>
          <img 
            src={imageURL} 
            alt="Upload" 
            style={{ maxWidth: '100%', height: 'auto' }}
          />
        </div>
      )}
      
      {isLoading && <p>Classifying image...</p>}
      
      {results.length > 0 && (
        <div>
          <h3>Predictions:</h3>
          <ul>
            {results.map((result, index) => (
              <li key={index}>
                {result.className}: {(result.probability * 100).toFixed(2)}%
              </li>
            ))}
          </ul>
        </div>
      )}
      
      {!model && <p>Loading AI model...</p>}
    </div>
  );
};

export default ImageClassifier;
EOF

echo "ImageClassifier component created!"
```

#### Object Detection Component
```bash
# Crear componente de detección de objetos
cat > src/components/ObjectDetector.js << 'EOF'
import React, { useState, useRef, useEffect } from 'react';
import * as tf from '@tensorflow/tfjs';
import * as cocoSsd from '@tensorflow-models/coco-ssd';

const ObjectDetector = () => {
  const [model, setModel] = useState(null);
  const [imageURL, setImageURL] = useState('');
  const [predictions, setPredictions] = useState([]);
  const canvasRef = useRef();
  const imageRef = useRef();

  useEffect(() => {
    const loadModel = async () => {
      console.log('Loading COCO-SSD model...');
      const loadedModel = await cocoSsd.load();
      setModel(loadedModel);
      console.log('Object detection model loaded');
    };
    loadModel();
  }, []);

  const detectObjects = async (imageElement) => {
    if (model && imageElement) {
      const predictions = await model.detect(imageElement);
      setPredictions(predictions);
      drawBoundingBoxes(predictions, imageElement);
    }
  };

  const drawBoundingBoxes = (predictions, imageElement) => {
    const canvas = canvasRef.current;
    const ctx = canvas.getContext('2d');
    
    canvas.width = imageElement.width;
    canvas.height = imageElement.height;
    
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.drawImage(imageElement, 0, 0);
    
    predictions.forEach(prediction => {
      const [x, y, width, height] = prediction.bbox;
      
      // Draw bounding box
      ctx.strokeStyle = '#00FF00';
      ctx.lineWidth = 2;
      ctx.strokeRect(x, y, width, height);
      
      // Draw label
      ctx.fillStyle = '#00FF00';
      ctx.font = '16px Arial';
      ctx.fillText(
        `${prediction.class} (${Math.round(prediction.score * 100)}%)`,
        x,
        y > 20 ? y - 5 : y + 20
      );
    });
  };

  const handleImageUpload = (event) => {
    const file = event.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onload = (e) => {
        setImageURL(e.target.result);
        
        const img = new Image();
        img.onload = () => {
          imageRef.current = img;
          detectObjects(img);
        };
        img.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }
  };

  return (
    <div style={{ padding: '20px', maxWidth: '800px', margin: '0 auto' }}>
      <h2>AI Object Detector</h2>
      
      <input
        type="file"
        accept="image/*"
        onChange={handleImageUpload}
        style={{ marginBottom: '20px' }}
      />
      
      {imageURL && (
        <div style={{ position: 'relative', marginBottom: '20px' }}>
          <canvas
            ref={canvasRef}
            style={{ 
              maxWidth: '100%', 
              height: 'auto',
              border: '1px solid #ccc'
            }}
          />
        </div>
      )}
      
      {predictions.length > 0 && (
        <div>
          <h3>Detected Objects:</h3>
          <ul>
            {predictions.map((prediction, index) => (
              <li key={index}>
                {prediction.class}: {Math.round(prediction.score * 100)}% confidence
              </li>
            ))}
          </ul>
        </div>
      )}
      
      {!model && <p>Loading object detection model...</p>}
    </div>
  );
};

export default ObjectDetector;
EOF

echo "ObjectDetector component created!"
```

### React with OpenAI API

#### Chat Component with OpenAI
```bash
# Instalar axios para llamadas API
npm install axios

# Crear componente de chat AI
cat > src/components/AIChat.js << 'EOF'
import React, { useState, useRef, useEffect } from 'react';
import axios from 'axios';

const AIChat = () => {
  const [messages, setMessages] = useState([]);
  const [inputMessage, setInputMessage] = useState('');
  const [isLoading, setIsLoading] = useState(false);
  const messagesEndRef = useRef(null);

  const scrollToBottom = () => {
    messagesEndRef.current?.scrollIntoView({ behavior: "smooth" });
  };

  useEffect(() => {
    scrollToBottom();
  }, [messages]);

  const sendMessage = async () => {
    if (!inputMessage.trim()) return;

    const userMessage = { role: 'user', content: inputMessage };
    setMessages(prev => [...prev, userMessage]);
    setInputMessage('');
    setIsLoading(true);

    try {
      // Note: En producción, las llamadas a OpenAI deberían ir a través de tu backend
      // para mantener segura tu API key
      const response = await axios.post('/api/chat', {
        messages: [...messages, userMessage]
      });

      const aiMessage = { 
        role: 'assistant', 
        content: response.data.message 
      };
      
      setMessages(prev => [...prev, aiMessage]);
    } catch (error) {
      console.error('Error sending message:', error);
      const errorMessage = { 
        role: 'assistant', 
        content: 'Sorry, there was an error processing your message.' 
      };
      setMessages(prev => [...prev, errorMessage]);
    }

    setIsLoading(false);
  };

  const handleKeyPress = (event) => {
    if (event.key === 'Enter' && !event.shiftKey) {
      event.preventDefault();
      sendMessage();
    }
  };

  return (
    <div style={{ 
      maxWidth: '600px', 
      margin: '0 auto', 
      padding: '20px',
      height: '600px',
      display: 'flex',
      flexDirection: 'column'
    }}>
      <h2>AI Chat Assistant</h2>
      
      <div style={{ 
        flex: 1, 
        overflowY: 'auto', 
        border: '1px solid #ccc', 
        padding: '10px',
        marginBottom: '10px'
      }}>
        {messages.map((message, index) => (
          <div 
            key={index} 
            style={{ 
              marginBottom: '10px',
              padding: '8px',
              backgroundColor: message.role === 'user' ? '#e3f2fd' : '#f5f5f5',
              borderRadius: '8px',
              alignSelf: message.role === 'user' ? 'flex-end' : 'flex-start'
            }}
          >
            <strong>{message.role === 'user' ? 'You' : 'AI'}:</strong>
            <div style={{ marginTop: '4px' }}>{message.content}</div>
          </div>
        ))}
        
        {isLoading && (
          <div style={{ 
            padding: '8px',
            backgroundColor: '#f5f5f5',
            borderRadius: '8px',
            fontStyle: 'italic'
          }}>
            AI is typing...
          </div>
        )}
        
        <div ref={messagesEndRef} />
      </div>
      
      <div style={{ display: 'flex', gap: '10px' }}>
        <textarea
          value={inputMessage}
          onChange={(e) => setInputMessage(e.target.value)}
          onKeyPress={handleKeyPress}
          placeholder="Type your message here..."
          style={{ 
            flex: 1, 
            minHeight: '60px', 
            padding: '8px',
            border: '1px solid #ccc',
            borderRadius: '4px'
          }}
          disabled={isLoading}
        />
        <button 
          onClick={sendMessage}
          disabled={isLoading || !inputMessage.trim()}
          style={{ 
            padding: '10px 20px',
            backgroundColor: '#007bff',
            color: 'white',
            border: 'none',
            borderRadius: '4px',
            cursor: 'pointer'
          }}
        >
          Send
        </button>
      </div>
    </div>
  );
};

export default AIChat;
EOF

echo "AIChat component created!"
```

### React with Custom AI Models

#### Sentiment Analysis Component
```bash
# Instalar biblioteca de análisis de sentimientos
npm install sentiment

# Crear componente de análisis de sentimientos
cat > src/components/SentimentAnalyzer.js << 'EOF'
import React, { useState } from 'react';
import Sentiment from 'sentiment';

const SentimentAnalyzer = () => {
  const [text, setText] = useState('');
  const [result, setResult] = useState(null);
  const sentiment = new Sentiment();

  const analyzeText = () => {
    if (text.trim()) {
      const analysis = sentiment.analyze(text);
      setResult(analysis);
    }
  };

  const getSentimentLabel = (score) => {
    if (score > 0) return { label: 'Positive', color: '#4caf50' };
    if (score < 0) return { label: 'Negative', color: '#f44336' };
    return { label: 'Neutral', color: '#ff9800' };
  };

  const sentimentInfo = result ? getSentimentLabel(result.score) : null;

  return (
    <div style={{ padding: '20px', maxWidth: '600px', margin: '0 auto' }}>
      <h2>AI Sentiment Analyzer</h2>
      
      <div style={{ marginBottom: '20px' }}>
        <textarea
          value={text}
          onChange={(e) => setText(e.target.value)}
          placeholder="Enter text to analyze sentiment..."
          style={{
            width: '100%',
            height: '100px',
            padding: '10px',
            border: '1px solid #ccc',
            borderRadius: '4px',
            fontSize: '14px'
          }}
        />
      </div>
      
      <button
        onClick={analyzeText}
        disabled={!text.trim()}
        style={{
          padding: '10px 20px',
          backgroundColor: '#007bff',
          color: 'white',
          border: 'none',
          borderRadius: '4px',
          cursor: 'pointer',
          marginBottom: '20px'
        }}
      >
        Analyze Sentiment
      </button>
      
      {result && (
        <div style={{ 
          border: '1px solid #ccc', 
          borderRadius: '8px', 
          padding: '20px',
          backgroundColor: '#f9f9f9'
        }}>
          <h3>Analysis Results</h3>
          
          <div style={{ marginBottom: '15px' }}>
            <strong>Sentiment: </strong>
            <span style={{ 
              color: sentimentInfo.color, 
              fontSize: '18px',
              fontWeight: 'bold'
            }}>
              {sentimentInfo.label}
            </span>
          </div>
          
          <div style={{ marginBottom: '10px' }}>
            <strong>Score:</strong> {result.score}
          </div>
          
          <div style={{ marginBottom: '10px' }}>
            <strong>Comparative:</strong> {result.comparative.toFixed(3)}
          </div>
          
          {result.positive.length > 0 && (
            <div style={{ marginBottom: '10px' }}>
              <strong>Positive words:</strong> {result.positive.join(', ')}
            </div>
          )}
          
          {result.negative.length > 0 && (
            <div style={{ marginBottom: '10px' }}>
              <strong>Negative words:</strong> {result.negative.join(', ')}
            </div>
          )}
          
          <div>
            <strong>Word count:</strong> {result.tokens.length}
          </div>
        </div>
      )}
    </div>
  );
};

export default SentimentAnalyzer;
EOF

echo "SentimentAnalyzer component created!"
```

### React Custom Hooks for AI

#### Custom Hook for AI Model Loading
```bash
# Crear custom hook para cargar modelos AI
cat > src/hooks/useAIModel.js << 'EOF'
import { useState, useEffect } from 'react';

const useAIModel = (modelLoader, dependencies = []) => {
  const [model, setModel] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    let mounted = true;

    const loadModel = async () => {
      try {
        setLoading(true);
        setError(null);
        
        console.log('Loading AI model...');
        const loadedModel = await modelLoader();
        
        if (mounted) {
          setModel(loadedModel);
          console.log('AI model loaded successfully');
        }
      } catch (err) {
        console.error('Error loading AI model:', err);
        if (mounted) {
          setError(err);
        }
      } finally {
        if (mounted) {
          setLoading(false);
        }
      }
    };

    loadModel();

    return () => {
      mounted = false;
    };
  }, dependencies);

  return { model, loading, error };
};

export default useAIModel;
EOF

# Crear custom hook para predicciones
cat > src/hooks/usePrediction.js << 'EOF'
import { useState, useCallback } from 'react';

const usePrediction = (model) => {
  const [prediction, setPrediction] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);

  const predict = useCallback(async (input) => {
    if (!model) {
      setError(new Error('Model not loaded'));
      return;
    }

    try {
      setLoading(true);
      setError(null);
      
      const result = await model.predict(input);
      setPrediction(result);
      
      return result;
    } catch (err) {
      console.error('Prediction error:', err);
      setError(err);
    } finally {
      setLoading(false);
    }
  }, [model]);

  return { prediction, loading, error, predict };
};

export default usePrediction;
EOF

echo "AI custom hooks created!"
```

### React AI Dashboard

#### Create AI Dashboard Component
```bash
# Crear componente dashboard AI
cat > src/components/AIDashboard.js << 'EOF'
import React, { useState } from 'react';
import ImageClassifier from './ImageClassifier';
import ObjectDetector from './ObjectDetector';
import SentimentAnalyzer from './SentimentAnalyzer';
import AIChat from './AIChat';

const AIDashboard = () => {
  const [activeTab, setActiveTab] = useState('image-classifier');

  const tabs = [
    { id: 'image-classifier', label: 'Image Classifier', component: ImageClassifier },
    { id: 'object-detector', label: 'Object Detector', component: ObjectDetector },
    { id: 'sentiment-analyzer', label: 'Sentiment Analyzer', component: SentimentAnalyzer },
    { id: 'ai-chat', label: 'AI Chat', component: AIChat }
  ];

  const ActiveComponent = tabs.find(tab => tab.id === activeTab)?.component;

  return (
    <div style={{ minHeight: '100vh', backgroundColor: '#f5f5f5' }}>
      {/* Header */}
      <header style={{ 
        backgroundColor: '#1976d2', 
        color: 'white', 
        padding: '20px',
        textAlign: 'center'
      }}>
        <h1>AI/ML Dashboard</h1>
        <p>Explore different AI capabilities in React</p>
      </header>

      {/* Navigation Tabs */}
      <nav style={{ 
        backgroundColor: 'white', 
        padding: '0 20px',
        borderBottom: '1px solid #ddd'
      }}>
        <div style={{ 
          display: 'flex', 
          gap: '0',
          maxWidth: '1200px',
          margin: '0 auto'
        }}>
          {tabs.map((tab) => (
            <button
              key={tab.id}
              onClick={() => setActiveTab(tab.id)}
              style={{
                padding: '15px 20px',
                border: 'none',
                backgroundColor: activeTab === tab.id ? '#1976d2' : 'transparent',
                color: activeTab === tab.id ? 'white' : '#666',
                cursor: 'pointer',
                borderBottom: activeTab === tab.id ? '3px solid #1976d2' : '3px solid transparent',
                fontSize: '14px',
                fontWeight: activeTab === tab.id ? 'bold' : 'normal'
              }}
            >
              {tab.label}
            </button>
          ))}
        </div>
      </nav>

      {/* Main Content */}
      <main style={{ 
        maxWidth: '1200px', 
        margin: '0 auto',
        padding: '20px'
      }}>
        {ActiveComponent && <ActiveComponent />}
      </main>

      {/* Footer */}
      <footer style={{ 
        backgroundColor: '#333', 
        color: 'white', 
        padding: '20px',
        textAlign: 'center',
        marginTop: '40px'
      }}>
        <p>AI/ML Dashboard built with React & TensorFlow.js</p>
      </footer>
    </div>
  );
};

export default AIDashboard;
EOF

echo "AIDashboard component created!"
```

### Integration Scripts

#### Setup Script for AI React App
```bash
#!/bin/bash
# setup_ai_react_app.sh
echo "Setting up AI-powered React application..."

# Crear nueva app React si no existe
if [ ! -f "package.json" ]; then
    echo "Creating new React app..."
    npx create-react-app ai-react-app
    cd ai-react-app
else
    echo "Using existing React project..."
fi

# Instalar dependencias AI/ML
echo "Installing AI/ML dependencies..."
npm install @tensorflow/tfjs @tensorflow/tfjs-vis
npm install @tensorflow-models/mobilenet @tensorflow-models/coco-ssd
npm install sentiment axios

# Crear estructura de carpetas
mkdir -p src/components src/hooks src/services

# Copiar componentes (los componentes ya fueron creados arriba)
echo "Components created successfully!"

# Actualizar App.js para usar el dashboard
cat > src/App.js << 'EOF'
import React from 'react';
import AIDashboard from './components/AIDashboard';
import './App.css';

function App() {
  return (
    <div className="App">
      <AIDashboard />
    </div>
  );
}

export default App;
EOF

# Actualizar App.css
cat > src/App.css << 'EOF'
.App {
  text-align: left;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
}

button:hover {
  opacity: 0.8;
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
EOF

echo "AI React app setup completed!"
echo "Run 'npm start' to start the development server"
```

### Performance Optimization for AI in React

#### Web Worker for AI Processing
```bash
# Crear Web Worker para procesamiento AI
cat > public/aiWorker.js << 'EOF'
// Web Worker para procesamiento AI intensivo
importScripts('https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js');

let model = null;

// Cargar modelo en el worker
const loadModel = async (modelUrl) => {
  try {
    model = await tf.loadLayersModel(modelUrl);
    postMessage({ type: 'MODEL_LOADED', success: true });
  } catch (error) {
    postMessage({ type: 'MODEL_LOADED', success: false, error: error.message });
  }
};

// Procesar predicción
const predict = async (inputData) => {
  if (!model) {
    postMessage({ type: 'PREDICTION_ERROR', error: 'Model not loaded' });
    return;
  }

  try {
    const tensor = tf.tensor(inputData);
    const prediction = model.predict(tensor);
    const result = await prediction.data();
    
    tensor.dispose();
    prediction.dispose();
    
    postMessage({ type: 'PREDICTION_RESULT', result: Array.from(result) });
  } catch (error) {
    postMessage({ type: 'PREDICTION_ERROR', error: error.message });
  }
};

// Escuchar mensajes del hilo principal
self.addEventListener('message', (event) => {
  const { type, data } = event.data;
  
  switch (type) {
    case 'LOAD_MODEL':
      loadModel(data.modelUrl);
      break;
    case 'PREDICT':
      predict(data.input);
      break;
    default:
      console.log('Unknown message type:', type);
  }
});
EOF

# Crear hook para usar Web Worker
cat > src/hooks/useAIWorker.js << 'EOF'
import { useState, useEffect, useRef } from 'react';

const useAIWorker = () => {
  const [worker, setWorker] = useState(null);
  const [modelLoaded, setModelLoaded] = useState(false);
  const [loading, setLoading] = useState(false);
  const resolveRef = useRef();
  const rejectRef = useRef();

  useEffect(() => {
    const aiWorker = new Worker('/aiWorker.js');
    
    aiWorker.onmessage = (event) => {
      const { type, success, result, error } = event.data;
      
      switch (type) {
        case 'MODEL_LOADED':
          setModelLoaded(success);
          if (success) {
            console.log('AI model loaded in worker');
          } else {
            console.error('Error loading model:', error);
          }
          break;
          
        case 'PREDICTION_RESULT':
          setLoading(false);
          if (resolveRef.current) {
            resolveRef.current(result);
          }
          break;
          
        case 'PREDICTION_ERROR':
          setLoading(false);
          if (rejectRef.current) {
            rejectRef.current(new Error(error));
          }
          break;
      }
    };

    setWorker(aiWorker);

    return () => {
      aiWorker.terminate();
    };
  }, []);

  const loadModel = (modelUrl) => {
    if (worker) {
      worker.postMessage({ type: 'LOAD_MODEL', data: { modelUrl } });
    }
  };

  const predict = (input) => {
    return new Promise((resolve, reject) => {
      if (!worker || !modelLoaded) {
        reject(new Error('Worker or model not ready'));
        return;
      }

      resolveRef.current = resolve;
      rejectRef.current = reject;
      setLoading(true);
      
      worker.postMessage({ type: 'PREDICT', data: { input } });
    });
  };

  return { loadModel, predict, modelLoaded, loading };
};

export default useAIWorker;
EOF

echo "AI Worker setup completed!"
```
