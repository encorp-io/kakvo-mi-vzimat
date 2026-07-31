# Какво ми взима държавата 🇧🇬

Професионален калкулатор за данъци и осигуровки в България, показващ как промените в данъчното законодателство през 2026 година ще засегнат вашата заплата.

![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4-38bdf8?logo=tailwind-css)
![Tests](https://img.shields.io/badge/Tests-32%20passed-success)

## 🎯 Основни функционалности

- **Точни изчисления**: Базирани на официалните данъчни ставки за 2025 и 2026
- **Пълна разбивка**: Детайлна информация за всички осигуровки и данъци
- **Разходи за работодател**: Показва колко струва служител на работодателя
- **Покупателна способност**: Сравнение с реални продукти
- **SEO оптимизиран**: Пълна оптимизация за търсачки
- **Респонсивен дизайн**: Работи перфектно на всички устройства
- **100% типизиран**: Изцяло написан на TypeScript
- **Unit tested**: Пълно тестово покритие на бизнес логиката

## 🚀 Бърз старт

### Инсталация

```bash
# Клонирайте репозиторито
git clone https://github.com/yourusername/kakvomivzimat.git

# Влезте в директорията
cd kakvomivzimat

# Инсталирайте зависимостите
npm install

# Стартирайте development сървъра
npm run dev
```

Отворете [http://localhost:3000](http://localhost:3000) във вашия браузър.

### Тестване

```bash
# Пуснете всички тестове
npm test

# Пуснете тестовете в watch режим
npm run test:watch
```

## 📊 Данъчни промени 2025 → 2026

> От 1 януари 2026 официалната валута в България е еврото. Всички суми в
> калкулатора и в тази документация са в EUR.

Бюджет 2026 променя **само** максималния осигурителен доход. Всички осигурителни
ставки и подоходният данък остават непроменени спрямо 2025 година.

### Максимален осигурителен доход (МОД)
- **2025**: 2,111.46 EUR (брутна заплата)
- **2026**: 2,300 EUR (брутна заплата)
- **Промяна**: +188.54 EUR (+8.9%)

### Осигуровки за служителя (без промяна за 2026)
- Пенсии: 6.58%
- ОЗМ (Общо заболяване и майчинство): 1.4%
- Безработица: 0.4%
- ДЗПО (Допълнително задължително пенсионно осигуряване): 2.2%
- Здравно осигуряване: 3.2%
- **Общо**: 13.78%

### Осигуровки за работодателя (без промяна за 2026)
- Пенсии: 8.22%
- ОЗМ: 2.1%
- Безработица: 0.6%
- ДЗПО: 2.8%
- ТЗПБ (Трудова злополука и професионална болест): 0.4%
- Здравно осигуряване: 4.8%
- **Общо**: 18.92%

### Данък върху доходите на физическите лица
- **2025 и 2026**: 10% (без промяна)

### Кого засяга промяната

Осигуровките се дължат само върху брутна заплата до МОД. Затова:

- **Брутна заплата под 2,111.46 EUR** – нищо не се променя.
- **Брутна заплата между 2,111.46 EUR и 2,300 EUR** – осигуровки се дължат върху
  цялата брутна заплата, а не само до стария таван.
- **Брутна заплата над 2,300 EUR** – максимален ефект: 25.98 EUR/месец повече
  осигуровки за служителя (23.38 EUR по-малко нетно след данъка) и 35.67
  EUR/месец повече разход за работодателя.

## 🏗️ Архитектура

### Технологичен стек

- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 3.4
- **Testing**: Jest + ts-jest
- **Deployment**: Vercel (препоръчително)

### Структура на проекта

```
kakvomivzimat/
├── app/                          # Next.js App Router
│   ├── layout.tsx               # Root layout с SEO metadata
│   ├── page.tsx                 # Главна страница
│   └── globals.css              # Глобални стилове
├── components/                   # React компоненти
│   ├── SalaryCalculatorForm.tsx # Форма за въвеждане на заплата
│   ├── ResultsDisplay.tsx       # Показване на резултати
│   └── ProductComparison.tsx    # Сравнение с продукти
├── lib/                         # Бизнес логика
│   ├── SalaryCalculator.ts      # Основен калкулатор клас
│   └── SalaryCalculator.test.ts # Unit tests
├── public/                      # Статични файлове
├── .gitignore
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── next.config.ts
├── jest.config.js
└── README.md
```

## 💻 Основни компоненти

### SalaryCalculator класа

Основният изчислителен клас, който съдържа цялата бизнес логика:

```typescript
import { salaryCalculator } from '@/lib/SalaryCalculator';

// Сравнение между 2025 и 2026
const comparison = salaryCalculator.compareSalaryBetweenYears(2000);

console.log(comparison.netSalaryDifference); // -23.38 EUR
console.log(comparison.annualNetSalaryDifference); // -280.56 EUR
console.log(comparison.percentageChange); // -1.17%
```

### Ключови методи

#### `calculateNetFromGross(grossSalary, config)`
Изчислява нетна заплата от брутна заплата.

```typescript
const result = calculator.calculateNetFromGross(5000, TAX_CONFIG_2025);
// Връща детайлна разбивка на всички осигуровки и данъци
```

#### `compareSalaryBetweenYears(netSalary2025)`
Сравнява заплати между 2025 и 2026 година.

```typescript
const comparison = calculator.compareSalaryBetweenYears(2000);
// Връща пълно сравнение с всички разлики
```

#### `calculateProductLoss(annualDifference, productPrice)`
Изчислява колко продукти могат да бъдат закупени с годишната разлика.

```typescript
const breads = calculator.calculateProductLoss(-280.56, 1.20);
// Връща 233 (хляба)
```

## 🧪 Тестване

Проектът има пълно тестово покритие на бизнес логиката:

- ✅ 32 unit теста
- ✅ Тестване на конфигурации за 2025 и 2026
- ✅ Тестване на изчисления под/над максимален осигурителен доход
- ✅ Тестване на edge cases
- ✅ Тестване на реални сценарии

### Примери за тестове

```bash
npm test

# Очакван изход:
# PASS lib/SalaryCalculator.test.ts
#   SalaryCalculator
#     Tax Configuration
#       ✓ 2025 configuration should have correct values
#       ✓ 2026 configuration should have correct values
#     ...
#   Test Suites: 1 passed, 1 total
#   Tests:       32 passed, 32 total
```

## 🎨 Дизайн и UX

### Цветова палитра

Проектът използва тъмна тема с акцент върху червени цветове, за да предаде негативното чувство от загубата на пари:

- **Основен фон**: Черно към тъмно сиво градиент
- **Акцент**: Червени тонове (danger-500 до danger-900)
- **Вторичен акцент**: Оранжеви тонове за продукти
- **Текст**: Бяло и сиви нюанси

### Responsive дизайн

- Mobile-first подход
- Breakpoints: sm (640px), md (768px), lg (1024px), xl (1280px)
- Оптимизиран за телефони, таблети и десктопи

## 🔧 Конфигурация

### Персонализиране на данъчни ставки

Можете лесно да промените данъчните ставки, като създадете custom конфигурация:

```typescript
import { SalaryCalculator, TaxConfig } from '@/lib/SalaryCalculator';

const customConfig: TaxConfig = {
  year: 2027,
  maxInsurableIncome: 5000,
  employee: {
    pension: 0.08,
    sickness: 0.015,
    unemployment: 0.005,
    supplementaryPension: 0.025,
    health: 0.035,
  },
  employer: {
    pension: 0.10,
    sickness: 0.025,
    unemployment: 0.007,
    supplementaryPension: 0.03,
    occupationalAccidents: 0.005,
    health: 0.05,
  },
  incomeTaxRate: 0.12,
};

const calculator = new SalaryCalculator(customConfig, customConfig);
```

### Персонализиране на продукти

Редактирайте `components/ProductComparison.tsx`:

```typescript
const PRODUCTS: Product[] = [
  { name: 'Хляб', emoji: '🍞', price: 2.5, unit: 'хляб' },
  { name: 'Вашият продукт', emoji: '🎯', price: 10.0, unit: 'бр.' },
  // ... добавете повече продукти
];
```

## 📈 SEO Оптимизация

Проектът е напълно оптимизиран за търсачки:

- ✅ Semantic HTML
- ✅ Meta tags (Open Graph, Twitter Cards)
- ✅ Structured data (JSON-LD)
- ✅ Responsive design
- ✅ Fast page load
- ✅ Accessibility (ARIA labels)
- ✅ Server-side rendering (SSR)

## 🚀 Деплоймънт

### Vercel (Препоръчително)

```bash
# Инсталирайте Vercel CLI
npm i -g vercel

# Deploy
vercel
```

### Други платформи

Проектът е Next.js приложение и може да бъде деплойнат на:
- Netlify
- AWS Amplify
- DigitalOcean App Platform
- Railway
- Render

## 📝 Лиценз

MIT License - вижте LICENSE файл за детайли.

## 👨‍💻 Автор

**Martin Kuvandzhiev**

Създадено с ❤️ за българските работещи хора.

### 🤖 AI Development

Този проект е разработен изцяло от AI, използвайки [AI Software Development Rules of encorp.ai](https://encorp.ai).

**Технологии**:
- Claude Code (Anthropic)
- AI-assisted development workflow
- Automated testing and documentation
- Professional code generation

## 🤝 Допринасяне

Pull requests са добре дошли! За значителни промени, моля първо отворете issue, за да обсъдим какво бихте искали да промените.

### Как да допринесете

1. Fork-нете проекта
2. Създайте feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit-нете промените (`git commit -m 'Add some AmazingFeature'`)
4. Push-нете към branch-а (`git push origin feature/AmazingFeature`)
5. Отворете Pull Request

## 📞 Обратна връзка

Имате въпроси или предложения? Отворете issue в GitHub!

---

**Важно**: Този калкулатор предоставя приблизителни изчисления базирани на публично достъпна информация за данъчните ставки. За точна информация за вашата индивидуална ситуация, моля консултирайте се със счетоводител или данъчен консултант.
