# Font Test SVG Collection

## 1. Basic Font Family Test
```xml
<svg width="400" height="300" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="380" height="280" fill="#f0f0f0" stroke="#333" stroke-width="2"/>
  <text x="200" y="40" text-anchor="middle" font-family="Arial" font-size="16" fill="black">
    This is Arial Font
  </text>
  <text x="200" y="70" text-anchor="middle" font-family="Arial" font-size="16" font-weight="bold" fill="black">
    Bold
  </text>
  <text x="200" y="100" text-anchor="middle" font-family="Arial" font-size="16" font-style="italic" fill="black">
    Italic
  </text>
  <text x="200" y="130" text-anchor="middle" font-family="Arial" font-size="16" font-weight="bold" font-style="italic" fill="black">
    Bold Italic
  </text>
  <text x="200" y="160" text-anchor="middle" font-family="Arial" font-size="16" text-decoration="underline" fill="black">
    Underline
  </text>
  <text x="200" y="190" text-anchor="middle" font-family="Arial" font-size="16" text-decoration="line-through" fill="black">
    Strikethrough
  </text>
  <text x="200" y="220" text-anchor="middle" font-family="Arial" font-size="12" fill="gray">
    Font size 12
  </text>
  <text x="200" y="250" text-anchor="middle" font-family="Arial" font-size="20" fill="gray">
    Font size 20
  </text>
</svg>
```

## 2. Roboto Font Test
```xml
<svg width="400" height="300" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="380" height="280" fill="#e8f4f8" stroke="#2196F3" stroke-width="2"/>
  <text x="200" y="40" text-anchor="middle" font-family="Roboto" font-size="16" fill="#1976D2">
    This is Roboto Font
  </text>
  <text x="200" y="70" text-anchor="middle" font-family="Roboto" font-size="16" font-weight="bold" fill="#1976D2">
    Bold
  </text>
  <text x="200" y="100" text-anchor="middle" font-family="Roboto" font-size="16" font-style="italic" fill="#1976D2">
    Italic
  </text>
  <text x="200" y="130" text-anchor="middle" font-family="Roboto" font-size="16" font-weight="bold" font-style="italic" fill="#1976D2">
    Bold Italic
  </text>
  <text x="200" y="160" text-anchor="middle" font-family="Roboto" font-size="16" text-decoration="underline" fill="#1976D2">
    Underline
  </text>
  <text x="200" y="190" text-anchor="middle" font-family="Roboto" font-size="16" text-decoration="line-through" fill="#1976D2">
    Strikethrough
  </text>
  <text x="200" y="220" text-anchor="middle" font-family="Roboto" font-size="14" fill="#666">
    Copyright © 2025 Test
  </text>
  <text x="200" y="250" text-anchor="middle" font-family="Roboto" font-size="14" fill="#666">
    Unicode: ñáéíóú ¿¡
  </text>
</svg>
```

## 3. Times New Roman Test
```xml
<svg width="400" height="300" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="380" height="280" fill="#fff8dc" stroke="#8B4513" stroke-width="2"/>
  <text x="200" y="40" text-anchor="middle" font-family="Times New Roman" font-size="16" fill="#8B4513">
    This is Times New Roman Font
  </text>
  <text x="200" y="70" text-anchor="middle" font-family="Times New Roman" font-size="16" font-weight="bold" fill="#8B4513">
    Bold
  </text>
  <text x="200" y="100" text-anchor="middle" font-family="Times New Roman" font-size="16" font-style="italic" fill="#8B4513">
    Italic
  </text>
  <text x="200" y="130" text-anchor="middle" font-family="Times New Roman" font-size="16" font-weight="bold" font-style="italic" fill="#8B4513">
    Bold Italic
  </text>
  <text x="200" y="160" text-anchor="middle" font-family="Times New Roman" font-size="16" text-decoration="underline" fill="#8B4513">
    Underline
  </text>
  <text x="200" y="190" text-anchor="middle" font-family="Times New Roman" font-size="16" text-decoration="line-through" fill="#8B4513">
    Strikethrough
  </text>
  <text x="200" y="220" text-anchor="middle" font-family="Times New Roman" font-size="14" fill="#A0522D">
    Serif font characteristics
  </text>
  <text x="200" y="250" text-anchor="middle" font-family="Times New Roman" font-size="14" fill="#A0522D">
    Traditional typography
  </text>
</svg>
```

## 4. Text Anchor Test
```xml
<svg width="500" height="200" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="480" height="180" fill="#f5f5f5" stroke="#333" stroke-width="2"/>
  
  <!-- Reference lines -->
  <line x1="100" y1="20" x2="100" y2="180" stroke="red" stroke-width="1" stroke-dasharray="2,2"/>
  <line x1="250" y1="20" x2="250" y2="180" stroke="red" stroke-width="1" stroke-dasharray="2,2"/>
  <line x1="400" y1="20" x2="400" y2="180" stroke="red" stroke-width="1" stroke-dasharray="2,2"/>
  
  <!-- Text anchor start -->
  <text x="100" y="50" text-anchor="start" font-family="Arial" font-size="14" fill="black">
    text-anchor="start"
  </text>
  <text x="100" y="75" text-anchor="start" font-family="Arial" font-size="14" font-weight="bold" fill="blue">
    Bold at start
  </text>
  
  <!-- Text anchor middle -->
  <text x="250" y="50" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    text-anchor="middle"
  </text>
  <text x="250" y="75" text-anchor="middle" font-family="Arial" font-size="14" font-style="italic" fill="green">
    Italic at middle
  </text>
  
  <!-- Text anchor end -->
  <text x="400" y="50" text-anchor="end" font-family="Arial" font-size="14" fill="black">
    text-anchor="end"
  </text>
  <text x="400" y="75" text-anchor="end" font-family="Arial" font-size="14" font-weight="bold" font-style="italic" fill="purple">
    Bold Italic at end
  </text>
  
  <!-- Baseline tests -->
  <line x1="50" y1="130" x2="450" y2="130" stroke="gray" stroke-width="1"/>
  <text x="100" y="130" text-anchor="start" font-family="Arial" font-size="16" fill="black">
    Baseline test
  </text>
  <text x="250" y="130" text-anchor="middle" font-family="Arial" font-size="20" fill="red">
    Larger text
  </text>
  <text x="400" y="130" text-anchor="end" font-family="Arial" font-size="12" fill="blue">
    Smaller text
  </text>
</svg>
```

## 5. Unicode and Special Characters Test
```xml
<svg width="450" height="350" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="430" height="330" fill="#fafafa" stroke="#666" stroke-width="2"/>
  <text x="225" y="40" text-anchor="middle" font-family="Arial" font-size="18" font-weight="bold" fill="black">
    Unicode Character Test
  </text>
  
  <text x="225" y="70" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Copyright © 2025
  </text>
  <text x="225" y="95" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Trademark ™ and Registered ®
  </text>
  <text x="225" y="120" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Currency: $ € £ ¥ ¢
  </text>
  <text x="225" y="145" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Math: ± × ÷ ° ¼ ½ ¾
  </text>
  <text x="225" y="170" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Accented: café résumé naïve
  </text>
  <text x="225" y="195" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Spanish: ¿Cómo está? ¡Excelente!
  </text>
  <text x="225" y="220" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Quotes: "Hello" 'World' „Test"
  </text>
  <text x="225" y="245" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Dashes: — – - and ellipsis…
  </text>
  <text x="225" y="270" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Arrows: ← → ↑ ↓ ↔
  </text>
  <text x="225" y="295" text-anchor="middle" font-family="Arial" font-size="14" fill="black">
    Symbols: ♪ ♫ ★ ☆ ♥ ♦ ♣ ♠
  </text>
</svg>
```

## 6. Baseline Alignment Test
```xml
<svg width="600" height="400" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="580" height="380" fill="#f9f9f9" stroke="#333" stroke-width="2"/>
  <text x="300" y="40" text-anchor="middle" font-family="Arial" font-size="18" font-weight="bold" fill="black">
    Baseline Alignment Test
  </text>
  
  <!-- Reference line -->
  <line x1="50" y1="100" x2="550" y2="100" stroke="red" stroke-width="2"/>
  <text x="30" y="105" font-family="Arial" font-size="10" fill="red">baseline</text>
  
  <!-- Different baseline alignments -->
  <text x="100" y="100" dominant-baseline="alphabetic" font-family="Arial" font-size="16" fill="black">alphabetic</text>
  <text x="200" y="100" dominant-baseline="middle" font-family="Arial" font-size="16" fill="blue">middle</text>
  <text x="300" y="100" dominant-baseline="hanging" font-family="Arial" font-size="16" fill="green">hanging</text>
  <text x="400" y="100" dominant-baseline="text-before-edge" font-family="Arial" font-size="16" fill="purple">before-edge</text>
  
  <!-- Another reference line -->
  <line x1="50" y1="180" x2="550" y2="180" stroke="red" stroke-width="2"/>
  <text x="30" y="185" font-family="Arial" font-size="10" fill="red">baseline</text>
  
  <!-- Test with different font sizes -->
  <text x="100" y="180" dominant-baseline="alphabetic" font-family="Arial" font-size="12" fill="black">Size 12</text>
  <text x="200" y="180" dominant-baseline="alphabetic" font-family="Arial" font-size="16" fill="black">Size 16</text>
  <text x="300" y="180" dominant-baseline="alphabetic" font-family="Arial" font-size="20" fill="black">Size 20</text>
  <text x="450" y="180" dominant-baseline="alphabetic" font-family="Arial" font-size="24" fill="black">Size 24</text>
  
  <!-- Mathematical baseline test -->
  <line x1="50" y1="260" x2="550" y2="260" stroke="red" stroke-width="2"/>
  <text x="30" y="265" font-family="Arial" font-size="10" fill="red">baseline</text>
  
  <text x="100" y="260" dominant-baseline="mathematical" font-family="Arial" font-size="16" fill="black">Mathematical</text>
  <text x="250" y="260" dominant-baseline="central" font-family="Arial" font-size="16" fill="blue">Central</text>
  <text x="350" y="260" dominant-baseline="ideographic" font-family="Arial" font-size="16" fill="green">Ideographic</text>
  
  <!-- Descender test -->
  <line x1="50" y1="320" x2="550" y2="320" stroke="red" stroke-width="2"/>
  <text x="30" y="325" font-family="Arial" font-size="10" fill="red">baseline</text>
  <text x="100" y="320" dominant-baseline="alphabetic" font-family="Arial" font-size="18" fill="black">gjpqy descenders</text>
  <text x="350" y="320" dominant-baseline="alphabetic" font-family="Arial" font-size="18" font-style="italic" fill="blue">gjpqy italic</text>
</svg>
```

## 7. Color and Size Variations
```xml
<svg width="500" height="300" xmlns="http://www.w3.org/2000/svg">
  <rect x="10" y="10" width="480" height="280" fill="#ffffff" stroke="#ddd" stroke-width="2"/>
  <text x="250" y="35" text-anchor="middle" font-family="Arial" font-size="18" font-weight="bold" fill="black">
    Color and Size Variations
  </text>
  
  <!-- Size progression -->
  <text x="50" y="70" font-family="Arial" font-size="8" fill="black">Size 8</text>
  <text x="50" y="90" font-family="Arial" font-size="10" fill="black">Size 10</text>
  <text x="50" y="115" font-family="Arial" font-size="12" fill="black">Size 12</text>
  <text x="50" y="145" font-family="Arial" font-size="14" fill="black">Size 14</text>
  <text x="50" y="180" font-family="Arial" font-size="16" fill="black">Size 16</text>
  <text x="50" y="220" font-family="Arial" font-size="18" fill="black">Size 18</text>
  <text x="50" y="265" font-family="Arial" font-size="20" fill="black">Size 20</text>
  
  <!-- Color variations -->
  <text x="250" y="80" font-family="Arial" font-size="14" fill="red">Red Text</text>
  <text x="250" y="105" font-family="Arial" font-size="14" fill="green">Green Text</text>
  <text x="250" y="130" font-family="Arial" font-size="14" fill="blue">Blue Text</text>
  <text x="250" y="155" font-family="Arial" font-size="14" fill="purple">Purple Text</text>
  <text x="250" y="180" font-family="Arial" font-size="14" fill="orange">Orange Text</text>
  <text x="250" y="205" font-family="Arial" font-size="14" fill="#666666">Gray Text</text>
  <text x="250" y="230" font-family="Arial" font-size="14" fill="#FF6B6B">Custom Color</text>
  <text x="250" y="255" font-family="Arial" font-size="14" fill="#4ECDC4">Another Custom</text>
</svg>
```

## Usage Instructions

Save each SVG as a separate file:
- `font-test-arial.svg`
- `font-test-roboto.svg` 
- `font-test-times.svg`
- `font-test-anchors.svg`
- `font-test-unicode.svg`
- `font-test-baselines.svg`
- `font-test-colors.svg`

These test files will help you verify:
- Font family rendering
- Bold, italic, underline, strikethrough styles
- Text anchoring (start, middle, end)
- Unicode character support
- Baseline alignment options
- Color and size variations
- Special characters like copyright symbols

Load these in your SVG renderer to compare the STB_TrueType output against the SDL_TTF reference.