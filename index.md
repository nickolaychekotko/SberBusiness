<!DOCTYPE html>
<!-- saved from url=(0115)file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html -->
<html lang="ru"><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>СберБизнес.Старт - Интерфейс</title>
    <script src="./index_files/saved_resource"></script>
    <script src="./index_files/chart.js"></script>
    <link href="./index_files/css2" rel="stylesheet">
    <style>
        /* Base styles for the document body */
        body {
            font-family: 'Inter', sans-serif; /* Use Inter, a modern sans-serif font */
            scroll-behavior: smooth;
        }

        /* Styles for the main content, controlling page switching */
        .page-content {
            display: none; /* Hidden by default */
        }
        .page-content.active {
            display: block; /* Display when active */
        }

        /* Styles for chart containers (if used) */
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px; /* Maximum width for charts */
            margin-left: auto;
            margin-right: auto;
            height: 250px; /* Base height for charts */
            max-height: 300px; /* Maximum height for charts */
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 300px;
                max-height: 350px;
            }
        }

        /* Styles for cards */
        .card {
            background-color: white;
            border-radius: 0.75rem; /* Rounded corners */
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); /* Material Design-like shadow */
            padding: 1.5rem;
            margin-bottom: 1.5rem;
        }

        /* Styles for large icons */
        .icon-large {
            font-size: 2.5rem;
            line-height: 1;
        }

        /* Styles for flowchart steps (if used) */
        .flowchart-step {
            border: 2px solid;
            padding: 0.75rem;
            text-align: center;
            border-radius: 0.5rem;
            margin-bottom: 0.75rem;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9rem;
        }
        .flowchart-arrow {
            font-size: 1.5rem;
            text-align: center;
            margin-bottom: 0.5rem;
            color: #6C757D; /* Grey color for arrows */
        }

        /* Styles for modals */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        .modal-content {
            background-color: white;
            padding: 2rem;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            max-width: 500px;
            width: 90%;
            text-align: center;
        }

        /* Updated Sberbank colors */
        .sber-green-bg {
            background-color: #21A038; /* Sber Green */
        }
        .sber-green-text {
            color: #21A038;
        }
        .sber-malachite-bg {
            background-color: #107F8C; /* Malachite */
        }
        .sber-malachite-text {
            color: #107F8C;
        }
        .sber-sea-wave-bg {
            background-color: #21A19A; /* Sea Wave */
        }
        .sber-sea-wave-text {
            color: #21A19A;
        }
        .sber-clover-bg {
            background-color: #31C2A7; /* Clover */
        }
        .sber-clover-text {
            color: #31C2A7;
        }
        .btn-primary {
            @apply sber-green-bg text-white font-semibold py-2 px-4 rounded-lg hover:opacity-90 transition duration-200;
        }
        .btn-secondary {
            @apply sber-malachite-bg text-white font-semibold py-2 px-4 rounded-lg hover:opacity-90 transition duration-200;
        }

        /* AI Assistant styles */
        .ai-assistant-button {
            position: fixed;
            bottom: 1.5rem;
            right: 1.5rem;
            background-color: #21A038; /* Sber Green */
            color: white;
            border-radius: 9999px; /* Fully circular */
            width: 64px; /* Button size */
            height: 64px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            cursor: pointer;
            transition: background-color 0.2s ease-in-out;
            z-index: 999; /* On top of other elements */
        }
        .ai-assistant-button:hover {
            background-color: #1a8f30; /* Slightly darker on hover */
        }

        .ai-chat-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .ai-chat-window {
            background-color: white;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            width: 90%;
            max-width: 450px; /* Max chat width */
            height: 70%;
            max-height: 600px; /* Max chat height */
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .chat-header {
            background-color: #107F8C; /* Malachite */
            color: white;
            padding: 1rem 1.5rem;
            font-weight: 600;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-top-left-radius: 0.75rem;
            border-top-right-radius: 0.75rem;
        }

        .chat-messages {
            flex-grow: 1;
            padding: 1rem 1.5rem;
            overflow-y: auto;
            background-color: #F8F9FA; /* Light grey background for messages */
        }

        .message-bubble {
            max-width: 80%;
            padding: 0.75rem 1rem;
            border-radius: 0.75rem;
            margin-bottom: 0.75rem;
            line-height: 1.4;
        }

        .message-user {
            background-color: #E9ECEF; /* Very light grey */
            align-self: flex-end;
            margin-left: auto;
            color: #212529;
        }

        .message-ai {
            background-color: #D4EDDA; /* Light green */
            align-self: flex-start;
            margin-right: auto;
            color: #212529;
        }

        .chat-input-area {
            padding: 1rem 1.5rem;
            border-top: 1px solid #CED4DA; /* Light grey separator */
            display: flex;
            align-items: center;
            gap: 0.5rem;
            background-color: white;
        }

        .chat-input-area input {
            flex-grow: 1;
            padding: 0.75rem 1rem;
            border: 1px solid #CED4DA;
            border-radius: 0.5rem;
            outline: none;
            font-size: 0.9rem;
        }

        .chat-input-area button {
            background-color: #21A038; /* Sber Green */
            color: white;
            padding: 0.75rem 1rem;
            border-radius: 0.5rem;
            font-weight: 500;
            transition: background-color 0.2s ease-in-out;
        }
        .chat-input-area button:hover {
            background-color: #1a8f30;
        }

        /* Gradient styles */
        .gradient-green-blue {
            background: linear-gradient(to right, #21A038, #107F8C); /* From green to malachite */
            color: white;
        }
        .gradient-green-lightgreen {
            background: linear-gradient(to right, #21A038, #31C2A7); /* From green to clover */
            color: white;
        }
        .gradient-blue-darkblue {
            background: linear-gradient(to right, #107F8C, #0A5F6C); /* From malachite to darker blue */
            color: white;
        }
        .loading-dots span {
            animation: blink 1.4s infinite linear;
        }
        .loading-dots span:nth-child(2) {
            animation-delay: 0.2s;
        }
        .loading-dots span:nth-child(3) {
            animation-delay: 0.4s;
        }
        @keyframes blink {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }

        /* Styles for quiz and checklist */
        .quiz-option {
            background-color: #F8F9FA;
            border: 1px solid #CED4DA;
            border-radius: 0.5rem;
            padding: 0.75rem;
            margin-bottom: 0.5rem;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        .quiz-option:hover {
            background-color: #E9ECEF;
        }
        .quiz-option.selected {
            border-color: #21A038;
            background-color: #D4EDDA;
            font-weight: 500;
        }
        .quiz-feedback {
            margin-top: 0.75rem;
            padding: 0.5rem 1rem;
            border-radius: 0.5rem;
            font-weight: 500;
        }
        .quiz-feedback.correct {
            background-color: #D4EDDA;
            color: #1a8f30;
        }
        .quiz-feedback.incorrect {
            background-color: #F8D7DA;
            color: #DC3545;
        }

        .checklist-item {
            display: flex;
            align-items: center;
            background-color: #F8F9FA;
            border: 1px solid #CED4DA;
            border-radius: 0.5rem;
            padding: 0.75rem;
            margin-bottom: 0.5rem;
        }
        .checklist-item input[type="checkbox"] {
            margin-right: 0.75rem;
            width: 1.25rem;
            height: 1.25rem;
            accent-color: #21A038; /* Green checkbox */
        }

        /* Specific styles for the new dashboard layout */
        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr; /* Single column for mobile */
            gap: 1.5rem;
        }

        @media (min-width: 768px) { /* Medium screens and up */
            .dashboard-grid {
                grid-template-columns: 2fr 1fr; /* Two columns: main content and sidebar */
            }
            .main-content-area {
                display: grid;
                grid-template-columns: repeat(3, 1fr); /* Three columns for main content blocks */
                gap: 1.5rem;
            }
        }

        @media (max-width: 767px) { /* Mobile specific adjustments */
            .main-content-area {
                grid-template-columns: 1fr; /* Single column for mobile */
            }
        }

        .scroll-container {
            overflow-x: auto;
            white-space: nowrap;
            padding-bottom: 1rem; /* Space for scrollbar */
        }

        .scroll-item {
            display: inline-block;
            width: 90%; /* Adjust width for mobile scroll */
            max-width: 300px; /* Max width for each card */
            margin-right: 1rem;
            vertical-align: top; /* Align items at the top */
        }

        @media (min-width: 768px) {
            .scroll-item {
                width: auto; /* Let content define width on larger screens */
                min-width: 280px; /* Minimum width for desktop cards */
            }
        }
    </style>
<style>*, ::before, ::after{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgb(59 130 246 / 0.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }::backdrop{--tw-border-spacing-x:0;--tw-border-spacing-y:0;--tw-translate-x:0;--tw-translate-y:0;--tw-rotate:0;--tw-skew-x:0;--tw-skew-y:0;--tw-scale-x:1;--tw-scale-y:1;--tw-pan-x: ;--tw-pan-y: ;--tw-pinch-zoom: ;--tw-scroll-snap-strictness:proximity;--tw-gradient-from-position: ;--tw-gradient-via-position: ;--tw-gradient-to-position: ;--tw-ordinal: ;--tw-slashed-zero: ;--tw-numeric-figure: ;--tw-numeric-spacing: ;--tw-numeric-fraction: ;--tw-ring-inset: ;--tw-ring-offset-width:0px;--tw-ring-offset-color:#fff;--tw-ring-color:rgb(59 130 246 / 0.5);--tw-ring-offset-shadow:0 0 #0000;--tw-ring-shadow:0 0 #0000;--tw-shadow:0 0 #0000;--tw-shadow-colored:0 0 #0000;--tw-blur: ;--tw-brightness: ;--tw-contrast: ;--tw-grayscale: ;--tw-hue-rotate: ;--tw-invert: ;--tw-saturate: ;--tw-sepia: ;--tw-drop-shadow: ;--tw-backdrop-blur: ;--tw-backdrop-brightness: ;--tw-backdrop-contrast: ;--tw-backdrop-grayscale: ;--tw-backdrop-hue-rotate: ;--tw-backdrop-invert: ;--tw-backdrop-opacity: ;--tw-backdrop-saturate: ;--tw-backdrop-sepia: ;--tw-contain-size: ;--tw-contain-layout: ;--tw-contain-paint: ;--tw-contain-style: }/* ! tailwindcss v3.4.16 | MIT License | https://tailwindcss.com */*,::after,::before{box-sizing:border-box;border-width:0;border-style:solid;border-color:#e5e7eb}::after,::before{--tw-content:''}:host,html{line-height:1.5;-webkit-text-size-adjust:100%;-moz-tab-size:4;tab-size:4;font-family:ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";font-feature-settings:normal;font-variation-settings:normal;-webkit-tap-highlight-color:transparent}body{margin:0;line-height:inherit}hr{height:0;color:inherit;border-top-width:1px}abbr:where([title]){-webkit-text-decoration:underline dotted;text-decoration:underline dotted}h1,h2,h3,h4,h5,h6{font-size:inherit;font-weight:inherit}a{color:inherit;text-decoration:inherit}b,strong{font-weight:bolder}code,kbd,pre,samp{font-family:ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace;font-feature-settings:normal;font-variation-settings:normal;font-size:1em}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative;vertical-align:baseline}sub{bottom:-.25em}sup{top:-.5em}table{text-indent:0;border-color:inherit;border-collapse:collapse}button,input,optgroup,select,textarea{font-family:inherit;font-feature-settings:inherit;font-variation-settings:inherit;font-size:100%;font-weight:inherit;line-height:inherit;letter-spacing:inherit;color:inherit;margin:0;padding:0}button,select{text-transform:none}button,input:where([type=button]),input:where([type=reset]),input:where([type=submit]){-webkit-appearance:button;background-color:transparent;background-image:none}:-moz-focusring{outline:auto}:-moz-ui-invalid{box-shadow:none}progress{vertical-align:baseline}::-webkit-inner-spin-button,::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}summary{display:list-item}blockquote,dd,dl,figure,h1,h2,h3,h4,h5,h6,hr,p,pre{margin:0}fieldset{margin:0;padding:0}legend{padding:0}menu,ol,ul{list-style:none;margin:0;padding:0}dialog{padding:0}textarea{resize:vertical}input::placeholder,textarea::placeholder{opacity:1;color:#9ca3af}[role=button],button{cursor:pointer}:disabled{cursor:default}audio,canvas,embed,iframe,img,object,svg,video{display:block;vertical-align:middle}img,video{max-width:100%;height:auto}[hidden]:where(:not([hidden=until-found])){display:none}.fixed{position:fixed}.absolute{position:absolute}.relative{position:relative}.inset-0{inset:0px}.right-0{right:0px}.top-0{top:0px}.z-50{z-index:50}.col-span-1{grid-column:span 1 / span 1}.mx-auto{margin-left:auto;margin-right:auto}.mb-2{margin-bottom:0.5rem}.mb-4{margin-bottom:1rem}.mb-6{margin-bottom:1.5rem}.mb-8{margin-bottom:2rem}.mr-2{margin-right:0.5rem}.mr-4{margin-right:1rem}.mt-4{margin-top:1rem}.mt-8{margin-top:2rem}.mb-1{margin-bottom:0.25rem}.mb-3{margin-bottom:0.75rem}.ml-2{margin-left:0.5rem}.mt-1{margin-top:0.25rem}.mt-3{margin-top:0.75rem}.mt-6{margin-top:1.5rem}.mt-2{margin-top:0.5rem}.block{display:block}.inline-block{display:inline-block}.flex{display:flex}.grid{display:grid}.hidden{display:none}.h-\[150px\]{height:150px}.h-full{height:100%}.h-4{height:1rem}.h-32{height:8rem}.h-5{height:1.25rem}.h-8{height:2rem}.max-h-96{max-height:24rem}.min-h-screen{min-height:100vh}.w-64{width:16rem}.w-full{width:100%}.w-4{width:1rem}.w-5{width:1.25rem}.w-8{width:2rem}.min-w-full{min-width:100%}.max-w-7xl{max-width:80rem}.max-w-2xl{max-width:42rem}.flex-1{flex:1 1 0%}.list-inside{list-style-position:inside}.list-disc{list-style-type:disc}.grid-cols-1{grid-template-columns:repeat(1, minmax(0, 1fr))}.grid-cols-2{grid-template-columns:repeat(2, minmax(0, 1fr))}.flex-col{flex-direction:column}.items-start{align-items:flex-start}.items-center{align-items:center}.justify-center{justify-content:center}.justify-between{justify-content:space-between}.gap-4{gap:1rem}.gap-8{gap:2rem}.gap-2{gap:0.5rem}.space-x-3 > :not([hidden]) ~ :not([hidden]){--tw-space-x-reverse:0;margin-right:calc(0.75rem * var(--tw-space-x-reverse));margin-left:calc(0.75rem * calc(1 - var(--tw-space-x-reverse)))}.space-y-3 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.75rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0.75rem * var(--tw-space-y-reverse))}.space-y-4 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(1rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(1rem * var(--tw-space-y-reverse))}.space-y-2 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.5rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0.5rem * var(--tw-space-y-reverse))}.space-y-1 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0.25rem * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0.25rem * var(--tw-space-y-reverse))}.overflow-hidden{overflow:hidden}.overflow-x-auto{overflow-x:auto}.overflow-y-auto{overflow-y:auto}.rounded-lg{border-radius:0.5rem}.rounded{border-radius:0.25rem}.rounded-md{border-radius:0.375rem}.rounded-full{border-radius:9999px}.rounded-bl-lg{border-bottom-left-radius:0.5rem}.border{border-width:1px}.border-b{border-bottom-width:1px}.border-\[\#CED4DA\]{--tw-border-opacity:1;border-color:rgb(206 212 218 / var(--tw-border-opacity, 1))}.border-\[\#E9ECEF\]{--tw-border-opacity:1;border-color:rgb(233 236 239 / var(--tw-border-opacity, 1))}.bg-\[\#F8F9FA\]{--tw-bg-opacity:1;background-color:rgb(248 249 250 / var(--tw-bg-opacity, 1))}.bg-black{--tw-bg-opacity:1;background-color:rgb(0 0 0 / var(--tw-bg-opacity, 1))}.bg-white{--tw-bg-opacity:1;background-color:rgb(255 255 255 / var(--tw-bg-opacity, 1))}.bg-\[\#212529\]{--tw-bg-opacity:1;background-color:rgb(33 37 41 / var(--tw-bg-opacity, 1))}.bg-\[\#E9ECEF\]{--tw-bg-opacity:1;background-color:rgb(233 236 239 / var(--tw-bg-opacity, 1))}.bg-\[\#21A038\]{--tw-bg-opacity:1;background-color:rgb(33 160 56 / var(--tw-bg-opacity, 1))}.bg-\[\#CED4DA\]{--tw-bg-opacity:1;background-color:rgb(206 212 218 / var(--tw-bg-opacity, 1))}.bg-blue-500{--tw-bg-opacity:1;background-color:rgb(59 130 246 / var(--tw-bg-opacity, 1))}.bg-red-500{--tw-bg-opacity:1;background-color:rgb(239 68 68 / var(--tw-bg-opacity, 1))}.bg-opacity-20{--tw-bg-opacity:0.2}.bg-opacity-50{--tw-bg-opacity:0.5}.bg-gradient-to-r{background-image:linear-gradient(to right, var(--tw-gradient-stops))}.from-\[\#21A038\]{--tw-gradient-from:#21A038 var(--tw-gradient-from-position);--tw-gradient-to:rgb(33 160 56 / 0) var(--tw-gradient-to-position);--tw-gradient-stops:var(--tw-gradient-from), var(--tw-gradient-to)}.to-\[\#107F8C\]{--tw-gradient-to:#107F8C var(--tw-gradient-to-position)}.p-4{padding:1rem}.p-6{padding:1.5rem}.p-3{padding:0.75rem}.p-2{padding:0.5rem}.px-4{padding-left:1rem;padding-right:1rem}.py-2{padding-top:0.5rem;padding-bottom:0.5rem}.py-8{padding-top:2rem;padding-bottom:2rem}.px-6{padding-left:1.5rem;padding-right:1.5rem}.py-3{padding-top:0.75rem;padding-bottom:0.75rem}.px-2{padding-left:0.5rem;padding-right:0.5rem}.px-3{padding-left:0.75rem;padding-right:0.75rem}.py-1{padding-top:0.25rem;padding-bottom:0.25rem}.pr-2{padding-right:0.5rem}.text-left{text-align:left}.text-center{text-align:center}.text-right{text-align:right}.align-top{vertical-align:top}.text-2xl{font-size:1.5rem;line-height:2rem}.text-base{font-size:1rem;line-height:1.5rem}.text-lg{font-size:1.125rem;line-height:1.75rem}.text-sm{font-size:0.875rem;line-height:1.25rem}.text-xl{font-size:1.25rem;line-height:1.75rem}.text-xs{font-size:0.75rem;line-height:1rem}.font-bold{font-weight:700}.font-medium{font-weight:500}.font-semibold{font-weight:600}.uppercase{text-transform:uppercase}.leading-none{line-height:1}.tracking-wider{letter-spacing:0.05em}.text-\[\#212529\]{--tw-text-opacity:1;color:rgb(33 37 41 / var(--tw-text-opacity, 1))}.text-\[\#21A038\]{--tw-text-opacity:1;color:rgb(33 160 56 / var(--tw-text-opacity, 1))}.text-\[\#6C757D\]{--tw-text-opacity:1;color:rgb(108 117 125 / var(--tw-text-opacity, 1))}.text-blue-600{--tw-text-opacity:1;color:rgb(37 99 235 / var(--tw-text-opacity, 1))}.text-red-600{--tw-text-opacity:1;color:rgb(220 38 38 / var(--tw-text-opacity, 1))}.text-white{--tw-text-opacity:1;color:rgb(255 255 255 / var(--tw-text-opacity, 1))}.text-green-600{--tw-text-opacity:1;color:rgb(22 163 74 / var(--tw-text-opacity, 1))}.text-purple-600{--tw-text-opacity:1;color:rgb(147 51 234 / var(--tw-text-opacity, 1))}.text-red-500{--tw-text-opacity:1;color:rgb(239 68 68 / var(--tw-text-opacity, 1))}.text-\[\#21257D\]{--tw-text-opacity:1;color:rgb(33 37 125 / var(--tw-text-opacity, 1))}.text-yellow-600{--tw-text-opacity:1;color:rgb(202 138 4 / var(--tw-text-opacity, 1))}.shadow-lg{--tw-shadow:0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 10px 15px -3px var(--tw-shadow-color), 0 4px 6px -4px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.shadow-md{--tw-shadow:0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);--tw-shadow-colored:0 4px 6px -1px var(--tw-shadow-color), 0 2px 4px -2px var(--tw-shadow-color);box-shadow:var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow)}.transition{transition-property:color, background-color, border-color, fill, stroke, opacity, box-shadow, transform, filter, -webkit-text-decoration-color, -webkit-backdrop-filter;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow, transform, filter, backdrop-filter;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, opacity, box-shadow, transform, filter, backdrop-filter, -webkit-text-decoration-color, -webkit-backdrop-filter;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.transition-colors{transition-property:color, background-color, border-color, fill, stroke, -webkit-text-decoration-color;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke;transition-property:color, background-color, border-color, text-decoration-color, fill, stroke, -webkit-text-decoration-color;transition-timing-function:cubic-bezier(0.4, 0, 0.2, 1);transition-duration:150ms}.duration-200{transition-duration:200ms}.hover\:bg-\[\#E9ECEF\]:hover{--tw-bg-opacity:1;background-color:rgb(233 236 239 / var(--tw-bg-opacity, 1))}.hover\:bg-\[\#CED4DA\]:hover{--tw-bg-opacity:1;background-color:rgb(206 212 218 / var(--tw-bg-opacity, 1))}.hover\:bg-\[\#ADB5BD\]:hover{--tw-bg-opacity:1;background-color:rgb(173 181 189 / var(--tw-bg-opacity, 1))}.hover\:bg-opacity-90:hover{--tw-bg-opacity:0.9}.hover\:text-\[\#21A038\]:hover{--tw-text-opacity:1;color:rgb(33 160 56 / var(--tw-text-opacity, 1))}.hover\:underline:hover{-webkit-text-decoration-line:underline;text-decoration-line:underline}.hover\:opacity-90:hover{opacity:0.9}.focus\:border-\[\#21A038\]:focus{--tw-border-opacity:1;border-color:rgb(33 160 56 / var(--tw-border-opacity, 1))}.focus\:ring-\[\#21A038\]:focus{--tw-ring-opacity:1;--tw-ring-color:rgb(33 160 56 / var(--tw-ring-opacity, 1))}@media (min-width: 640px){.sm\:grid-cols-3{grid-template-columns:repeat(3, minmax(0, 1fr))}.sm\:grid-cols-2{grid-template-columns:repeat(2, minmax(0, 1fr))}.sm\:flex-row{flex-direction:row}.sm\:space-x-4 > :not([hidden]) ~ :not([hidden]){--tw-space-x-reverse:0;margin-right:calc(1rem * var(--tw-space-x-reverse));margin-left:calc(1rem * calc(1 - var(--tw-space-x-reverse)))}.sm\:space-y-0 > :not([hidden]) ~ :not([hidden]){--tw-space-y-reverse:0;margin-top:calc(0px * calc(1 - var(--tw-space-y-reverse)));margin-bottom:calc(0px * var(--tw-space-y-reverse))}}@media (min-width: 768px){.md\:col-span-1{grid-column:span 1 / span 1}.md\:col-span-3{grid-column:span 3 / span 3}.md\:col-span-2{grid-column:span 2 / span 2}.md\:col-span-full{grid-column:1 / -1}.md\:flex{display:flex}.md\:hidden{display:none}.md\:grid-cols-3{grid-template-columns:repeat(3, minmax(0, 1fr))}.md\:grid-cols-2{grid-template-columns:repeat(2, minmax(0, 1fr))}.md\:gap-6{gap:1.5rem}.md\:p-6{padding:1.5rem}.md\:px-6{padding-left:1.5rem;padding-right:1.5rem}.md\:text-2xl{font-size:1.5rem;line-height:2rem}.md\:text-3xl{font-size:1.875rem;line-height:2.25rem}.md\:text-base{font-size:1rem;line-height:1.5rem}.md\:text-lg{font-size:1.125rem;line-height:1.75rem}.md\:text-sm{font-size:0.875rem;line-height:1.25rem}}@media (min-width: 1024px){.lg\:col-span-1{grid-column:span 1 / span 1}.lg\:grid-cols-4{grid-template-columns:repeat(4, minmax(0, 1fr))}.lg\:grid-cols-3{grid-template-columns:repeat(3, minmax(0, 1fr))}.lg\:grid-cols-5{grid-template-columns:repeat(5, minmax(0, 1fr))}}</style></head>
<body class="bg-[#F8F9FA] text-[#212529] flex min-h-screen">

    <aside class="w-64 bg-white shadow-lg p-6 flex-col justify-between hidden md:flex">
        <div>
            <div class="text-2xl font-bold text-[#21A038] mb-8">СберБизнес.Старт</div>
            <nav>
                <ul>
                    <li class="mb-4">
                        <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="dashboard">
                            <span class="icon-large">🏠</span>
                            <span>Мой Бизнес</span>
                        </button>
                    </li>
                    <li class="mb-4">
                        <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="payments">
                            <span class="icon-large">💸</span>
                            <span>Платежи</span>
                        </button>
                    </li>
                    <li class="mb-4">
                        <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="accounts">
                            <span class="icon-large">💳</span>
                            <span>Счета</span>
                        </button>
                    </li>
                    <li class="mb-4">
                        <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="products">
                            <span class="icon-large">📦</span>
                            <span>Продукты и Сервисы</span>
                        </button>
                    </li>
                    <li class="mb-4">
                        <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="support">
                            <span class="icon-large">❓</span>
                            <span>Поддержка</span>
                        </button>
                    </li>
                    <li class="mb-4">
                        <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="sberguide">
                            <span class="icon-large">📚</span> <span>СберГайд</span>
                        </button>
                    </li>
                </ul>
            </nav>
        </div>
        <div class="mt-8">
            <button class="nav-link w-full py-2 px-4 rounded-lg flex items-center space-x-3 text-[#6C757D] hover:bg-[#E9ECEF] transition-colors duration-200 font-medium" data-page="settings">
                <span class="icon-large">⚙️</span>
                <span>Настройки</span>
            </button>
        </div>
    </aside>

    <main class="flex-1 p-4 md:p-6 flex flex-col">
        <header class="bg-white shadow-md p-4 flex justify-between items-center md:hidden mb-6 rounded-lg">
            <div class="text-xl font-bold text-[#21A038]">СберБизнес.Старт</div>
            <button id="mobile-menu-button" class="text-[#212529]">
                <span class="icon-large">☰</span>
            </button>
        </header>

        <div id="mobile-nav-overlay" class="fixed inset-0 bg-black bg-opacity-50 z-50 hidden md:hidden">
            <div class="bg-white w-64 h-full p-6 flex flex-col justify-between">
                <div>
                    <div class="text-2xl font-bold text-[#21A038] mb-8">СберБизнес.Старт</div>
                    <nav>
                        <ul>
                            <li class="mb-4">
                                <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="dashboard">
                                    <span class="icon-large">🏠</span>
                                    <span>Мой Бизнес</span>
                                </button>
                            </li>
                            <li class="mb-4">
                                <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="payments">
                                    <span class="icon-large">💸</span>
                                    <span>Платежи</span>
                                </button>
                            </li>
                            <li class="mb-4">
                                <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="accounts">
                                    <span class="icon-large">💳</span>
                                    <span>Счета</span>
                                </button>
                            </li>
                            <li class="mb-4">
                                <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="products">
                                    <span class="icon-large">📦</span>
                                    <span>Продукты и Сервисы</span>
                                </button>
                            </li>
                            <li class="mb-4">
                                <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="support">
                                    <span class="icon-large">❓</span>
                                    <span>Поддержка</span>
                                </button>
                            </li>
                            <li class="mb-4">
                                <button class="nav-link w-full text-left py-2 px-4 rounded-lg flex items-center space-x-3 hover:bg-[#E9ECEF] transition-colors duration-200 text-[#212529] font-medium" data-page="sberguide">
                                    <span class="icon-large">📚</span> <span>СберГайд</span>
                                </button>
                            </li>
                        </ul>
                    </nav>
                </div>
                <div class="mt-8">
                    <button class="nav-link w-full py-2 px-4 rounded-lg flex items-center space-x-3 text-[#6C757D] hover:bg-[#E9ECEF] transition-colors duration-200 font-medium" data-page="settings">
                        <span class="icon-large">⚙️</span>
                        <span>Настройки</span>
                    </button>
                </div>
            </div>
        </div>

        <section id="dashboard-page" class="page-content active">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Мой Бизнес</h1>

            <div class="card mb-6 p-6 bg-gradient-to-r from-[#21A038] to-[#107F8C] text-white">
                <h2 class="text-xl md:text-2xl font-bold mb-2">Добро пожаловать, Лев!</h2>
                <p class="text-lg mb-4">Ваш бизнес: Услуги для студентов, Екатеринбург</p>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                    <div class="bg-white bg-opacity-20 p-4 rounded-lg flex items-start space-x-3">
                        <span class="text-2xl">💬</span>
                        <div>
                            <p class="font-medium text-base">Ваши расходы на логистику выше на 14%</p>
                        </div>
                    </div>
                    <div class="bg-white bg-opacity-20 p-4 rounded-lg flex items-start space-x-3">
                        <span class="text-2xl">📊</span>
                        <div>
                            <p class="font-medium text-base">Популярность наборов с брендингом выросла на 31% — стоит протестировать?</p>
                        </div>
                    </div>
                    <div class="bg-white bg-opacity-20 p-4 rounded-lg flex items-start space-x-3">
                        <span class="text-2xl">💼</span>
                        <div>
                            <p class="font-medium text-base">Ваша ниша — сезонная. Следующий пик ожидается в августе. Планируйте закупки заранее</p>
                        </div>
                    </div>
                </div>
                <div class="flex flex-col sm:flex-row space-y-3 sm:space-y-0 sm:space-x-4">
                    <button class="bg-white text-[#21A038] font-semibold py-2 px-4 rounded-lg hover:opacity-90 transition duration-200 text-base">
                        📈 Сравнить с рынком
                    </button>
                    <button class="bg-white text-[#21A038] font-semibold py-2 px-4 rounded-lg hover:opacity-90 transition duration-200 text-base">
                        📚 Подобрать обучающие материалы
                    </button>
                    <button class="bg-white text-[#21A038] font-semibold py-2 px-4 rounded-lg hover:opacity-90 transition duration-200 text-base">
                        📞 Получить совет от ментора
                    </button>
                </div>
            </div>

            <div class="dashboard-grid">
                <div class="main-content-area">
                    <div class="card col-span-1">
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Пульс Рынка: Малый e-commerce / Наборы / Доставка</h2>
                        <div class="space-y-4 text-base">
                            <div class="flex justify-between items-center">
                                <span>Средний доход по нише:</span>
                                <span class="font-bold sber-green-text">74 000 ₽</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span>У Льва:</span>
                                <span class="font-bold sber-green-text">86 000 ₽</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span>Средние расходы:</span>
                                <span class="font-bold text-red-600">58 000 ₽</span>
                            </div>
                            <div class="flex justify-between items-center">
                                <span>У Льва:</span>
                                <span class="font-bold text-red-600">63 000 ₽</span>
                            </div>
                            <div class="chart-container h-[150px]">
                                <canvas id="marketSeasonalityChart"></canvas>
                            </div>
                            <p class="text-sm text-[#6C757D]">График сезонности (спрос)</p>
                            <h3 class="font-semibold text-[#212529] mt-4">Популярные модели:</h3>
                            <ul class="list-disc list-inside text-sm text-[#6C757D]">
                                <li>Модель подписки на товары для общаги — набирает популярность</li>
                                <li>В Екатеринбурге за месяц открыто +17 новых ИП в этой нише</li>
                                <li>Рост ниши: +18% в августе</li>
                            </ul>
                        </div>
                        <button class="w-full py-2 px-4 sber-malachite-bg text-white rounded-lg font-semibold hover:opacity-90 transition-colors duration-200 text-base mt-4">
                            Фильтровать по региону
                        </button>
                    </div>

                    <div class="card col-span-1">
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Тренды: Что важно сейчас для вашего бизнеса</h2>
                        <div class="scroll-container">
                            <div class="scroll-item card bg-[#F8F9FA] p-4 rounded-lg inline-block align-top mr-4">
                                <div class="flex items-center mb-2">
                                    <span class="icon-large text-blue-600 mr-2">📦</span>
                                    <h3 class="font-semibold text-lg text-[#212529]">Продукт</h3>
                                </div>
                                <p class="text-sm text-[#6C757D] mb-3">Добавьте опцию "RoomKit Pro" — спрос на премиум-наборы вырос на 30%.</p>
                                <button class="sber-malachite-text hover:underline text-sm font-medium">Углубиться</button>
                            </div>
                            <div class="scroll-item card bg-[#F8F9FA] p-4 rounded-lg inline-block align-top mr-4">
                                <div class="flex items-center mb-2">
                                    <span class="icon-large text-green-600 mr-2">💡</span>
                                    <h3 class="font-semibold text-lg text-[#212529]">Маркетинг</h3>
                                </div>
                                <p class="text-sm text-[#6C757D] mb-3">Пользователи WB в Екатеринбурге чаще ищут "всё для первокурсника" — добавьте SEO-описание.</p>
                                <button class="sber-malachite-text hover:underline text-sm font-medium">Углубиться</button>
                            </div>
                            <div class="scroll-item card bg-[#F8F9FA] p-4 rounded-lg inline-block align-top mr-4">
                                <div class="flex items-center mb-2">
                                    <span class="icon-large text-purple-600 mr-2">📈</span>
                                    <h3 class="font-semibold text-lg text-[#212529]">Цена</h3>
                                </div>
                                <p class="text-sm text-[#6C757D] mb-3">Поднимите цену на 5% — средний чек в регионе вырос до 2 900 ₽.</p>
                                <button class="sber-malachite-text hover:underline text-sm font-medium">Углубиться</button>
                            </div>
                        </div>
                    </div>

                    <div class="card col-span-1">
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Что делают другие предприниматели</h2>
                        <div class="space-y-4">
                            <div class="bg-[#F8F9FA] p-4 rounded-lg">
                                <p class="text-sm text-[#212529] mb-2">🧍‍♂️ **ИП из Перми** начал продажи аналогичных наборов — использует рекламу в TikTok</p>
                                <div class="flex space-x-3 text-sm text-[#6C757D]">
                                    <button class="flex items-center hover:text-[#21A038]">❤️ 5</button>
                                    <button class="flex items-center hover:text-[#21A038]">💬 2</button>
                                    <button class="flex items-center hover:text-[#21A038]">🔗 Подписаться</button>
                                </div>
                            </div>
                            <div class="bg-[#F8F9FA] p-4 rounded-lg">
                                <p class="text-sm text-[#212529] mb-2">🧍‍♀️ **Бизнес в Самаре** подключил Яндекс Доставку — расходы упали на 17%</p>
                                <div class="flex space-x-3 text-sm text-[#6C757D]">
                                    <button class="flex items-center hover:text-[#21A038]">❤️ 12</button>
                                    <button class="flex items-center hover:text-[#21A038]">💬 7</button>
                                    <button class="flex items-center hover:text-[#21A038]">🔗 Подписаться</button>
                                </div>
                            </div>
                            <div class="bg-[#F8F9FA] p-4 rounded-lg">
                                <p class="text-sm text-[#212529] mb-2">📣 **5 предпринимателей** в категории перешли на самовывоз — экономия 12 000 ₽/мес</p>
                                <div class="flex space-x-3 text-sm text-[#6C757D]">
                                    <button class="flex items-center hover:text-[#21A038]">❤️ 8</button>
                                    <button class="flex items-center hover:text-[#21A038]">💬 4</button>
                                    <button class="flex items-center hover:text-[#21A038]">🔗 Подписаться</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="card col-span-1 md:col-span-1">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Ваше комьюнити</h2>
                    <div class="space-y-3 mb-6">
                        <div class="p-3 bg-[#F8F9FA] rounded-lg flex justify-between items-center">
                            <span class="text-base">📍 Екатеринбург / E-commerce</span>
                            <span class="text-red-500 text-xl">🔥</span>
                        </div>
                        <div class="p-3 bg-[#F8F9FA] rounded-lg">
                            <span class="text-base">🏷️ Молодые предприниматели</span>
                        </div>
                        <div class="p-3 bg-[#F8F9FA] rounded-lg">
                            <span class="text-base">🧠 Продажи на маркетплейсах</span>
                        </div>
                    </div>
                    <div class="flex flex-col space-y-3">
                        <button class="w-full py-2 px-4 sber-green-bg text-white rounded-lg font-semibold hover:opacity-90 transition-colors duration-200 text-base">
                            Войти в чат
                        </button>
                        <button class="w-full py-2 px-4 sber-malachite-bg text-white rounded-lg font-semibold hover:opacity-90 transition-colors duration-200 text-base">
                            Задать вопрос
                        </button>
                        <button class="w-full py-2 px-4 bg-[#E9ECEF] text-[#212529] rounded-lg font-semibold hover:bg-[#CED4DA] transition-colors duration-200 text-base">
                            Найти ментора
                        </button>
                    </div>
                </div>
            </div>

            <footer class="bg-[#212529] text-white py-8 px-4 md:px-6 mt-8 rounded-lg">
                <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-8">
                    <div>
                        <h3 class="text-lg font-semibold mb-4">Сервисы</h3>
                        <ul class="space-y-2 text-sm">
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Сервисы для людей с особыми потребностями</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Сервис выставления счетов</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Размещение денежных средств</a></li>
                        </ul>
                    </div>

                    <div>
                        <h3 class="text-lg font-semibold mb-4">О банке и контакты</h3>
                        <ul class="space-y-2 text-sm mb-4">
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Частным клиентам</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">О банке</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Пресс-центр</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Закупки</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Инсайдерам банка</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Меры безопасности</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Вакансии</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Связаться с банком</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Политика обработки данных</a></li>
                        </ul>
                        <div class="text-sm">
                            <p class="mb-1">Бесплатные звонки с моб. телефонов (Билайн, Мегафон, МТС, СберМобайл, Tele2, Yota) на территории РФ</p>
                            <p class="font-bold text-xl mb-1">0321</p>
                            <p class="font-bold text-xl mb-1">+7 495 665-5-777</p>
                            <p class="text-xs">Звонки из-за рубежа (оплата согласно тарифу)</p>
                        </div>
                    </div>

                    <div>
                        <h3 class="text-lg font-semibold mb-4">Юридическая информация</h3>
                        <p class="text-sm mb-2">Россия, Москва, 117312, ул. Вавилова, 19</p>
                        <p class="text-sm mb-2">© 1997-2025 ПАО Сбербанк.</p>
                        <p class="text-sm mb-2">Генеральная лицензия на осуществление банковских операций от 11 августа 2015 года. Регистрационный номер 1481.</p>
                        <ul class="space-y-2 text-sm">
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Информация о процентных ставках по договорам банковского вклада с физическими лицами</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Информация, обязательная к размещению</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">Раскрытие информации о банке как о профессиональном участнике рынка ценных бумаг</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">На информационном ресурсе применяются рекомендательные технологии</a></li>
                        </ul>
                    </div>

                    <div class="lg:col-span-1 md:col-span-3">
                        <h3 class="text-lg font-semibold mb-4">Язык</h3>
                        <ul class="space-y-2 text-sm">
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">English</a></li>
                            <li><a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="hover:underline">中文版</a></li>
                        </ul>
                    </div>
                </div>
            </footer>
        </section>

        <section id="payments-page" class="page-content">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Платежи</h1>
            <p class="text-base md:text-lg text-[#6C757D] mb-8">Удобное создание и отслеживание всех ваших платежей.</p>

            <div class="grid grid-cols-1 gap-4 md:grid-cols-2 md:gap-6">
                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Создать новый платеж</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Быстро выполните платеж на расчётный счёт компании-контрагента.</p>
                    <div class="space-y-4">
                        <div>
                            <label for="inn" class="block text-sm font-medium text-[#212529] mb-1">ИНН или название компании</label>
                            <input type="text" id="inn" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Введите ИНН или название">
                            <p class="text-xs text-[#6C757D] mt-1">Дождитесь автозаполнения реквизитов (БИК, номер счёта).</p>
                        </div>
                        <div>
                            <label for="amount" class="block text-sm font-medium text-[#212529] mb-1">Сумма</label>
                            <input type="number" id="amount" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Например, 10000">
                        </div>
                        <div>
                            <label for="purpose" class="block text-sm font-medium text-[#212529] mb-1">Назначение платежа</label>
                            <textarea id="purpose" rows="3" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Например, Оплата за услуги по договору №123"></textarea>
                            <p class="text-xs text-[#6C757D] mt-1">Постарайтесь максимально полно описать назначение платежа.</p>
                        </div>
                        <div>
                            <label for="account_from" class="block text-sm font-medium text-[#212529] mb-1">Счет списания</label>
                            <select id="account_from" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                                <option>Расчетный счет (₽)</option>
                                <option>Валютный счет ($)</option>
                            </select>
                        </div>
                        <div class="flex items-center">
                            <input type="checkbox" id="save_template" class="h-4 w-4 text-[#21A038] rounded border-[#CED4DA] focus:ring-[#21A038]">
                            <label for="save_template" class="ml-2 text-sm text-[#212529]">Сохранить как шаблон (Совет: сохраняйте часто повторяющиеся платежи как шаблоны — это сократит время на ввод реквизитов.)</label>
                        </div>
                        <button id="submit-payment-button" class="w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Подтвердить и отправить</button>
                    </div>
                </div>

                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Мои шаблоны платежей</h2>
                    <div class="space-y-3 mb-6">
                        <div class="p-3 bg-[#F8F9FA] rounded-md flex justify-between items-center text-base">
                            <span>Оплата коробок (ИП Поставщик)</span>
                            <button class="sber-malachite-text hover:underline text-sm font-medium">Использовать</button>
                        </div>
                        <div class="p-3 bg-[#F8F9FA] rounded-md flex justify-between items-center text-base">
                            <span>Аренда мини-склада</span>
                            <button class="sber-malachite-text hover:underline text-sm font-medium">Использовать</button>
                        </div>
                    </div>
                    <button class="w-full py-2 px-4 bg-[#E9ECEF] text-[#212529] rounded-lg font-semibold hover:bg-[#CED4DA] transition-colors duration-200 text-base">Создать новый шаблон</button>

                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mt-8 mb-4">История платежей</h2>
                    <div class="overflow-x-auto">
                        <table class="min-w-full bg-white rounded-lg">
                            <thead>
                                <tr class="bg-[#E9ECEF] text-left text-sm text-[#6C757D] font-medium">
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-[#6C757D] uppercase tracking-wider">
                                    Дата
                                </th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-[#6C757D] uppercase tracking-wider">
                                    Получатель
                                </th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-[#6C757D] uppercase tracking-wider">
                                    Сумма
                                </th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-[#6C757D] uppercase tracking-wider">
                                    Статус
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr class="border-b border-[#E9ECEF]">
                                <td class="py-3 px-4 text-sm">20.05.2025</td>
                                <td class="py-3 px-4 text-sm">ООО "Поставщик"</td>
                                <td class="py-3 px-4 text-sm text-red-600">- 45 000 ₽</td>
                                <td class="py-3 px-4 text-sm sber-green-text">Исполнен</td>
                            </tr>
                            <tr class="border-b border-[#E9ECEF]">
                                <td class="py-3 px-4 text-sm">17.05.2025</td>
                                <td class="py-3 px-4 text-sm">Аренда склада</td>
                                <td class="py-3 px-4 text-sm text-red-600">- 5 000 ₽</td>
                                <td class="py-3 px-4 text-sm sber-malachite-text">Исполнен</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <button class="mt-4 sber-malachite-text hover:underline text-sm font-medium">Посмотреть всю историю</button>
            </div>
        </div></section>

        <section id="accounts-page" class="page-content">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Счета</h1>
            <p class="text-base md:text-lg text-[#6C757D] mb-8">Управляйте всеми вашими счетами и получайте выписки.</p>

            <div class="grid grid-cols-1 gap-4 md:grid-cols-2 md:gap-6">
                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Мои активные счета</h2>
                    <div class="space-y-4">
                        <div class="p-4 bg-[#F8F9FA] rounded-md border border-[#CED4DA]">
                            <div class="flex justify-between items-center mb-2">
                                <span class="font-bold text-lg">Расчетный счет (₽)</span>
                                <span class="sber-green-text font-bold text-lg">41 000 ₽</span>
                            </div>
                            <p class="text-sm text-[#6C757D]">Открыт: 3 месяца назад</p>
                            <button class="mt-3 sber-malachite-text hover:underline text-sm font-medium">Запросить выписку</button>
                        </div>
                    </div>
                    <button class="mt-6 w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Открыть новый счет</button>
                </div>

                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">СберКопилка для Налогов</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Автоматическое резервирование средств для уплаты налогов.</p>
                    <div class="space-y-3 mb-4">
                        <div class="flex justify-between items-center bg-[#F8F9FA] p-3 rounded-lg">
                            <div>
                                <p class="text-sm text-[#6C757D]">Процент резервирования</p>
                                <p class="font-bold text-lg text-[#212529]">6% от оборота</p>
                            </div>
                            <button class="sber-malachite-text hover:underline text-sm font-medium">Настроить</button>
                        </div>
                        <div class="flex justify-between items-center bg-[#F8F9FA] p-3 rounded-lg">
                            <div>
                                <p class="text-sm text-[#6C757D]">Накоплено для налогов</p>
                                <p class="font-bold text-lg text-[#21A038]">5 000 ₽</p>
                            </div>
                            <button class="sber-malachite-text hover:underline text-sm font-medium">История</button>
                        </div>
                        <div class="flex justify-between items-center bg-[#F8F9FA] p-3 rounded-lg">
                            <div>
                                <p class="text-sm text-[#6C757D]">Прогноз налога к уплате</p>
                                <p class="font-bold text-lg text-[#212529]">6 200 ₽</p>
                            </div>
                            <span class="icon text-yellow-600 text-xl">🔔</span>
                        </div>
                    </div>
                    <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Перейти к СберКопилке</button>
                </div>

                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Получение выписки по счёту</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Сформируйте и скачайте выписку по движению средств.</p>
                    <div class="space-y-4">
                        <div>
                            <label for="statement_account" class="block text-sm font-medium text-[#212529] mb-1">Выберите расчетный счет</label>
                            <select id="statement_account" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                                <option>Расчетный счет (₽)</option>
                                <option>Валютный счет ($)</option>
                            </select>
                        </div>
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label for="start_date" class="block text-sm font-medium text-[#212529] mb-1">Дата начала</label>
                                <input type="date" id="start_date" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                            </div>
                            <div>
                                <label for="end_date" class="block text-sm font-medium text-[#212529] mb-1">Дата окончания</label>
                                <input type="date" id="end_date" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                            </div>
                        </div>
                        <div>
                            <label for="file_format" class="block text-sm font-medium text-[#212529] mb-1">Формат файла</label>
                            <select id="file_format" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                                <option>PDF</option>
                                <option>CSV</option>
                            </select>
                        </div>
                        <button class="w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Сформировать</button>
                    </div>
                    <h3 class="text-lg font-semibold text-[#212529] mt-6 mb-3">Готовые выписки</h3>
                    <div class="space-y-3">
                        <div class="p-3 bg-[#F8F9FA] rounded-md flex justify-between items-center text-base">
                            <span>Выписка за Апрель 2025</span>
                            <button class="sber-malachite-text hover:underline text-sm font-medium">Скачать PDF</button>
                        </div>
                        <div class="p-3 bg-[#F8F9FA] rounded-md flex justify-between items-center text-base">
                            <span>Выписка за Март 2025</span>
                            <button class="sber-malachite-text hover:underline text-sm font-medium">Скачать PDF</button>
                        </div>
                    </div>
                    <p class="text-xs text-[#6C757D] mt-4">Совет: регулярно скачивайте ключевые отчёты для аналитики.</p>
                </div>
            </div>
        </section>

        <section id="products-page" class="page-content">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Продукты и Сервисы</h1>
            <p class="text-base md:text-lg text-[#6C757D] mb-8">Актуальные предложения Сбера для роста вашего бизнеса.</p>

            <div class="card mb-6">
                <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Курсы валют</h2>
                <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-5 gap-4 text-center">
                    <div class="bg-[#F8F9FA] p-3 rounded-lg">
                        <p class="font-bold text-lg text-[#212529]">USD</p>
                        <p class="text-sm text-[#6C757D]">86,45 ▲</p>
                    </div>
                    <div class="bg-[#F8F9FA] p-3 rounded-lg">
                        <p class="font-bold text-lg text-[#212529]">EUR</p>
                        <p class="text-sm text-[#6C757D]">95,89 ▲</p>
                    </div>
                    <div class="bg-[#F8F9FA] p-3 rounded-lg">
                        <p class="font-bold text-lg text-[#212529]">CNY</p>
                        <p class="text-sm text-[#6C757D]">11,55 ▲</p>
                    </div>
                    <div class="bg-[#F8F9FA] p-3 rounded-lg">
                        <p class="font-bold text-lg text-[#212529]">INR</p>
                        <p class="text-sm text-[#6C757D]">98,49 ▲</p>
                    </div>
                    <div class="bg-[#F8F9FA] p-3 rounded-lg">
                        <p class="font-bold text-lg text-[#21257D]">Au</p>
                        <p class="text-sm text-[#6C757D]">8 640,00 ▲</p>
                    </div>
                </div>
                <div class="mt-4 text-right">
                    <button class="sber-malachite-text font-medium hover:underline text-sm">Настроить виджеты</button>
                </div>
            </div>

            <div class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-3 md:gap-6">
                <div class="card">
                    <div class="sber-green-text icon-large mb-3">💰</div>
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">Расчетно-кассовое обслуживание</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Выберите тариф, который идеально подходит для вашего стартапа. Открытие счета за 5 минут.</p>
                    <ul class="list-disc list-inside text-[#6C757D] text-sm mb-4">
                        <li>Тариф "Легкий старт"</li>
                        <li>Бесплатное обслуживание первые 3 месяца</li>
                    </ul>
                    <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Оформить заявку</button>
                </div>

                <div class="card">
                    <div class="sber-green-text icon-large mb-3">📈</div>
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">Оформление кредита</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Выберите кредитный продукт, рассчитайте график и отправьте заявку.</p>
                    <ul class="list-disc list-inside text-[#6C757D] text-sm mb-4 space-y-1">
                        <li>Отфильтруйте предложения по сумме, сроку и цели.</li>
                        <li>В калькуляторе установите сумму и срок.</li>
                        <li>Заполните онлайн-анкету (сведения о компании, финансы, цель).</li>
                        <li>Прикрепите необходимые документы в PDF.</li>
                    </ul>
                    <p class="text-xs text-[#6C757D] mb-4">Совет: заранее подготовьте документы, чтобы ускорить подачу.</p>
                    <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Оформить заявку</button>
                    <button class="w-full py-2 px-4 bg-[#E9ECEF] text-[#212529] rounded-lg font-semibold hover:bg-[#CED4DA] transition-colors duration-200 text-base mt-2">Мои заявки</button>
                </div>

                <div class="card">
                    <div class="sber-green-text icon-large mb-3">🚚</div>
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">Заказ самоинкассации</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Закажите выезд курьера-инкассатора для забора наличных.</p>
                    <div class="space-y-3 mb-4">
                        <div>
                            <label for="pickup_address" class="block text-sm font-medium text-[#212529] mb-1">Адрес забора</label>
                            <input type="text" id="pickup_address" class="w-full p-2 border border-[#CED4DA] rounded-lg text-base" placeholder="Выберите сохраненный или введите новый">
                        </div>
                        <div>
                            <label for="cash_amount" class="block text-sm font-medium text-[#212529] mb-1">Сумма наличных и валюта</label>
                            <input type="text" id="cash_amount" class="w-full p-2 border border-[#CED4DA] rounded-lg text-base" placeholder="Например, 100 000 ₽">
                        </div>
                        <div>
                            <label for="pickup_datetime" class="block text-sm font-medium text-[#212529] mb-1">Дата и время приезда курьера</label>
                            <input type="datetime-local" id="pickup_datetime" class="w-full p-2 border border-[#CED4DA] rounded-lg text-base">
                        </div>
                    </div>
                    <p class="text-xs text-[#6C757D] mb-4">Совет: планируйте заказы заранее, чтобы выбрать удобное время.</p>
                    <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Заказать инкассацию</button>
                    <button class="w-full py-2 px-4 bg-[#E9ECEF] text-[#212529] rounded-lg font-semibold hover:bg-[#CED4DA] transition-colors duration-200 text-base mt-2">История заказов</button>
                </div>

                <div class="card">
                    <div class="sber-green-text icon-large mb-3">💳</div>
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">Бизнес-карты</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Удобные расчеты, снятие наличных и контроль расходов для вашего бизнеса.</p>
                    <ul class="list-disc list-inside text-[#6C757D] text-sm mb-4">
                        <li>Бесплатное обслуживание</li>
                        <li>Кэшбэк на бизнес-расходы</li>
                    </ul>
                    <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Заказать карту</button>
                </div>

                <div class="card">
                    <div class="sber-green-text icon-large mb-3">🛒</div>
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">Эквайринг</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Принимайте платежи от клиентов любым удобным способом: онлайн, по QR-коду или через терминал.</p>
                    <ul class="list-disc list-inside text-[#6C757D] text-sm mb-4">
                        <li>Низкие комиссии</li>
                        <li>Быстрое подключение</li>
                    </ul>
                    <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Подключить</button>
                </div>

                <div class="card">
                    <div class="sber-green-text icon-large mb-3">📊</div>
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">Онлайн-бухгалтерия</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Упростите ведение учета и сдачу отчетности с нашими партнерскими сервисами.</p>
                    <ul class="list-disc list-inside text-[#6C757D] text-sm mb-4">
                        <li>Автоматический расчет налогов</li>
                        <li>Формирование деклараций</li>
                    </ul>
                    <button class="w-full py-2 px-4 sber-malachite-bg text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Узнать подробнее</button>
                </div>

                <div class="card md:col-span-full">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Экосистема и Маркетплейс</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Единое окно управления бизнесом: от платежей до бухгалтерии и маркетинга.</p>
                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 mb-4">
                        <div class="bg-[#F8F9FA] p-3 rounded-lg flex items-center space-x-3">
                            <span class="icon text-green-600 text-xl">🔗</span>
                            <div>
                                <p class="font-medium text-[#212529] text-base">Интеграция с 1С-Бухгалтерией</p>
                                <p class="text-sm text-[#6C757D]">Автоэкспорт платежей, импорт счетов.</p>
                            </div>
                        </div>
                        <div class="bg-[#F8F9FA] p-3 rounded-lg flex items-center space-x-3">
                            <span class="icon text-blue-600 text-xl">🔗</span>
                            <div>
                                <p class="font-medium text-[#212529] text-base">Яндекс Бизнес / Метрика</p>
                                <p class="text-sm text-[#6C757D]">Таргет, реклама, аналитика по лидам.</p>
                            </div>
                        </div>
                        <div class="bg-[#F8F9FA] p-3 rounded-lg flex items-center space-x-3">
                            <span class="icon text-purple-600 text-xl">🔗</span>
                            <div>
                                <p class="font-medium text-[#212529] text-base">CRM-системы (amoCRM, Bitrix24)</p>
                                <p class="text-sm text-[#6C757D]">Интеграция для обработки заявок.</p>
                            </div>
                        </div>
                    </div>
                    <button class="w-full py-2 px-4 sber-malachite-bg text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Перейти в Маркетплейс</button>
                </div>
            </div>
        </section>

        <section id="support-page" class="page-content">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Поддержка</h1>
            <p class="text-base md:text-lg text-[#6C757D] mb-8">Мы всегда готовы помочь вам с любыми вопросами.</p>

            <div id="support-overview-screen">
                <div class="grid grid-cols-1 gap-4 md:grid-cols-2 md:gap-6">
                    <div class="card">
                        <div class="sber-green-text icon-large mb-3">📚</div>
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">База знаний / FAQ</h2>
                        <p class="text-sm md:text-base text-[#6C757D] mb-4">Найдите ответы на самые частые вопросы, посмотрите видеоуроки и изучите глоссарий.</p>
                        <input type="text" placeholder="Поиск по Базе знаний..." class="w-full p-2 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base mb-4">
                        <ul class="list-disc list-inside text-[#6C757D] text-sm mb-4 space-y-1">
                            <li><button class="text-left sber-malachite-text hover:underline font-medium knowledge-category-link" data-category="start">Начало работы</button></li>
                            <li><button class="text-left sber-malachite-text hover:underline font-medium knowledge-category-link" data-category="payments">Платежи и переводы</button></li>
                            <li><button class="text-left sber-malachite-text hover:underline font-medium knowledge-category-link" data-category="taxes">Налоги и отчетность</button></li>
                            <li><button class="text-left sber-malachite-text hover:underline font-medium knowledge-category-link" data-category="popular">Популярные вопросы</button></li>
                        </ul>
                        <p class="text-xs text-[#6C757D] mb-4">Короткие видеоуроки и интерактивные инструкции помогут быстрее разобраться.</p>
                        <button class="w-full py-2 px-4 sber-malachite-bg text-white rounded-lg font-semibold hover:opacity-90 transition-colors duration-200 text-base">Перейти в Базу знаний</button>
                    </div>

                    <div class="card">
                        <div class="sber-green-text icon-large mb-3">💬</div>
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Чат с поддержкой</h2>
                        <p class="text-sm md:text-base text-[#6C757D] mb-4">Получите быструю консультацию от наших специалистов в режиме реального времени.</p>
                        <div class="h-32 bg-[#F8F9FA] rounded-md p-3 mb-4 overflow-y-auto text-sm text-[#6C757D]">
                            <p>Оператор: Здравствуйте! Чем могу помочь?</p>
                            <p>Вы: Добрый день! У меня вопрос по заполнению платежного поручения.</p>
                        </div>
                        <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Начать чат</button>
                        <a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="block text-center sber-malachite-text hover:underline text-sm font-medium mt-2">История чатов</a>
                        <div class="mt-4 space-y-2">
                            <p class="text-sm font-medium text-[#212529]">Частые проблемы:</p>
                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-2">
                                <button class="py-2 px-3 bg-[#E9ECEF] text-[#212529] rounded-lg text-sm hover:bg-[#CED4DA] transition-colors duration-200">Не пришел платеж</button>
                                <button class="py-2 px-3 bg-[#E9ECEF] text-[#212529] rounded-lg text-sm hover:bg-[#CED4DA] transition-colors duration-200">Заблокирован аккаунт</button>
                                <button class="py-2 px-3 bg-[#E9ECEF] text-[#212529] rounded-lg text-sm hover:bg-[#CED4DA] transition-colors duration-200">Не работает сервис</button>
                            </div>
                        </div>
                    </div>

                    <div class="card">
                        <div class="sber-green-text icon-large mb-3">🤝</div>
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Сообщества и форумы</h2>
                        <p class="text-sm md:text-base text-[#6C757D] mb-4">Обсуждайте вопросы, делитесь опытом и получайте ответы от других предпринимателей и экспертов Сбера.</p>
                        <button class="w-full py-2 px-4 sber-malachite-bg text-white rounded-lg font-semibold hover:opacity-90 transition-colors duration-200 text-base">Перейти в сообщество</button>
                        <p class="text-xs text-[#6C757D] mt-4">Возможность обсуждения с другими предпринимателями. Ответы от модераторов / экспертов Сбера.</p>
                    </div>

                    <div class="card">
                        <div class="sber-green-text icon-large mb-3">📝</div>
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Обратная связь</h2>
                        <p class="text-sm md:text-base text-[#6C757D] mb-4">Ваше мнение помогает нам стать лучше! Оставьте свои предложения или сообщите об ошибке.</p>
                        <textarea rows="4" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Ваше сообщение..."></textarea>
                        <button class="mt-4 w-full py-2 px-4 bg-[#E9ECEF] text-[#212529] rounded-lg font-semibold hover:bg-[#CED4DA] transition-colors duration-200 text-base">Отправить</button>
                    </div>

                    <div class="card md:col-span-2">
                        <div class="sber-green-text icon-large mb-3">📞</div>
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Телефонная поддержка</h2>
                        <p class="text-sm md:text-base text-[#6C757D] mb-4">Свяжитесь с нами по телефону для оперативной консультации.</p>
                        <p class="text-2xl font-bold text-[#212529] mb-2">8 800 555-55-50</p>
                        <p class="text-sm text-[#6C757D] mb-4">График работы: Пн-Пт с 9:00 до 18:00 (МСК)</p>
                        <button class="w-full py-2 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Заказать обратный звонок</button>
                        <p class="text-xs text-[#6C757D] mt-4">Для VIP-клиентов доступен персональный менеджер.</p>
                    </div>
                </div>
            </div>

            <div id="knowledge-base-detail-screen" class="hidden">
                <button id="back-to-support-overview" class="btn-secondary mb-4">
                    <span class="icon">⬅️</span>
                    Вернуться в Поддержку
                </button>
                <div class="card">
                    <h2 id="kb-detail-title" class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3"></h2>
                    <div id="kb-detail-content" class="space-y-4 text-base text-[#212529]">
                        </div>
                </div>
            </div>
        </section>

        <section id="sberguide-page" class="page-content">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Путеводитель молодого предпринимателя</h1>
            <p class="text-base md:text-lg text-[#6C757D] mb-8">Пошаговый гайд по запуску и развитию вашего бизнеса со СберБизнес.Старт.</p>

            <div id="sberguide-overview-screen">
                <div class="card mb-8">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Ваш прогресс</h2>
                    <div class="w-full bg-[#E9ECEF] rounded-full h-4 mb-4">
                        <div id="sberguide-progress-bar" class="sber-green-bg h-4 rounded-full" style="width: 0%;"></div>
                    </div>
                    <p id="sberguide-progress-text" class="text-sm text-[#6C757D] text-center">0% пройдено (0 из 5 модулей)</p>
                </div>

                <div class="card mb-6">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Важное для бизнеса</h2>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div class="bg-[#F8F9FA] p-4 rounded-lg flex flex-col items-center text-center">
                            <img src="./index_files/FFFFFF" alt="Юридическая поддержка" class="mb-2 rounded-full">
                            <h3 class="text-lg font-semibold text-[#212529]">Юридическая поддержка бизнеса</h3>
                            <a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="text-sm sber-malachite-text hover:underline font-medium">Подробнее</a>
                        </div>
                        <div class="bg-[#F8F9FA] p-4 rounded-lg flex flex-col items-center text-center">
                            <img src="./index_files/FFFFFF(1)" alt="Отчетность в госорганы" class="mb-2 rounded-full">
                            <h3 class="text-lg font-semibold text-[#212529]">Отчётность в госорганы</h3>
                            <a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="text-sm sber-malachite-text hover:underline font-medium">Подробнее</a>
                        </div>
                        <div class="bg-[#F8F9FA] p-4 rounded-lg flex flex-col items-center text-center relative overflow-hidden">
                            <div class="absolute top-0 right-0 bg-red-500 text-white text-xs px-2 py-1 rounded-bl-lg">Новое</div>
                            <img src="./index_files/FFFFFF(2)" alt="Новости" class="mb-2 rounded-full">
                            <h3 class="text-lg font-semibold text-[#212529]">Маркировка звонков, 3-НДФЛ без штрафов, рост онлайн-продаж</h3>
                            <a href="file:///C:/Users/Nikolay/Downloads/Telegram%20Desktop/25%20%D0%BC%D0%B0%D1%8F%20%D0%A4%D0%98%D0%9D%D0%90%D0%9B.html#" class="text-sm sber-malachite-text hover:underline font-medium">Новости</a>
                        </div>
                    </div>
                </div>

                <div id="sberguide-modules-list" class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6">
                    </div>

                <div class="card mt-6">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Дополнительные ресурсы</h2>
                    <ul class="space-y-3">
                        <li>
                            <button class="flex items-center text-base font-medium sber-sea-wave-text hover:underline" onclick="sberGuide.showGlossaryModal()">
                                <span class="icon mr-2">🔗</span>
                                Глоссарий терминов для предпринимателей
                            </button>
                        </li>
                        <li>
                            <button class="flex items-center text-base font-medium sber-sea-wave-text hover:underline" onclick="sberGuide.showCalendarModal()">
                                <span class="icon mr-2">📅</span>
                                Календарь важных дат для бизнеса (налоги, отчетность)
                            </button>
                        </li>
                    </ul>
                </div>
            </div>

            <div id="sberguide-learning-screen" class="hidden">
                <button id="back-to-modules" class="btn-secondary mb-4">
                    <span class="icon">⬅️</span>
                    Вернуться к модулям
                </button>
                <div class="card">
                    <h2 id="learning-module-title" class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3"></h2>
                    <p id="learning-step-subtitle" class="text-sm md:text-base text-[#6C757D] mb-4"></p>
                    <div id="learning-step-content" class="space-y-4 mb-6">
                        </div>
                    <div class="flex justify-between items-center">
                        <button id="previous-step" class="btn-secondary hidden">
                            <span class="icon">⬅️</span>
                            Назад
                        </button>
                        <button id="next-step" class="btn-primary">
                            <span class="icon">➡️</span>
                            Далее
                        </button>
                        <button id="apply-now-button" class="btn-primary hidden">
                            <span class="icon">🛠</span>
                            Применить сейчас
                        </button>
                        <button id="complete-module-button" class="btn-primary hidden">
                            <span class="icon">✅</span>
                            Завершить модуль
                        </button>
                    </div>
                    <p id="learning-footer-progress" class="text-xs text-[#6C757D] mt-4 text-right"></p>
                </div>
            </div>

            <div id="sberguide-completion-screen" class="hidden text-center card py-8">
                <h2 class="text-2xl md:text-3xl font-bold sber-green-text mb-4">🎉 Модуль завершён! Молодец!</h2>
                <p id="completed-module-badge" class="text-xl font-semibold text-[#212529] mb-6"></p>
                <div class="flex flex-col sm:flex-row justify-center space-y-3 sm:space-y-0 sm:space-x-4">
                    <button id="go-to-next-module" class="btn-primary">
                        <span class="icon">✅</span>
                        Перейти к следующему модулю
                    </button>
                    <button class="btn-secondary" onclick="sberGuide.showOverview();">
                        <span class="icon">🏠</span>
                        Вернуться на главную СберГайда
                    </button>
                </div>
            </div>

        </section>

        <section id="settings-page" class="page-content">
            <h1 class="text-2xl md:text-3xl font-bold text-[#212529] mb-6">Настройки</h1>
            <p class="text-base md:text-lg text-[#6C757D] mb-8">Управляйте настройками вашего профиля, уведомлениями и безопасностью.</p>

            <div class="grid grid-cols-1 gap-4 md:grid-cols-2 md:gap-6">
                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Профиль бизнеса</h2>
                    <div class="space-y-4">
                        <div>
                            <label for="company_name" class="block text-sm font-medium text-[#212529] mb-1">Название компании</label>
                            <input type="text" id="company_name" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" value="RoomKit">
                        </div>
                        <div>
                            <label for="inn_settings" class="block text-sm font-medium text-[#212529] mb-1">ИНН</label>
                            <input type="text" id="inn_settings" class="w-full p-3 border border-[#CED4DA] rounded-lg bg-[#F8F9FA] text-[#6C757D] text-base" value="7700123456" readonly="">
                            <p class="text-xs text-[#6C757D] mt-1">ИНН нельзя изменить самостоятельно. Для изменения обратитесь в поддержку.</p>
                        </div>
                        <div>
                            <label for="contact_email" class="block text-sm font-medium text-[#212529] mb-1">Контактный email</label>
                            <input type="email" id="contact_email" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" value="lev.romanov@example.com">
                        </div>
                        <div>
                            <label for="contact_phone" class="block text-sm font-medium text-[#212529] mb-1">Контактный телефон</label>
                            <input type="tel" id="contact_phone" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" value="+7 (999) 123-45-67">
                        </div>
                        <button class="w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Сохранить изменения</button>
                    </div>
                </div>

                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Уведомления</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Настройте, какие уведомления вы хотите получать и каким способом.</p>
                    <div class="space-y-4">
                        <div class="flex items-center justify-between">
                            <label for="notify_payments" class="text-base text-[#212529]">О новых платежах</label>
                            <input type="checkbox" id="notify_payments" class="h-5 w-5 text-[#21A038] rounded border-[#CED4DA] focus:ring-[#21A038]" checked="">
                        </div>
                        <div class="flex items-center justify-between">
                            <label for="notify_taxes" class="text-base text-[#212529]">О сроках уплаты налогов</label>
                            <input type="checkbox" id="notify_taxes" class="h-5 w-5 text-[#21A038] rounded border-[#CED4DA] focus:ring-[#21A038]" checked="">
                        </div>
                        <div class="flex items-center justify-between">
                            <label for="notify_news" class="text-base text-[#212529]">О новостях и акциях</label>
                            <input type="checkbox" id="notify_news" class="h-5 w-5 text-[#21A038] rounded border-[#CED4DA] focus:ring-[#21A038]">
                        </div>
                        <div class="flex items-center justify-between">
                            <label for="notify_security" class="text-base text-[#212529]">О входе в аккаунт</label>
                            <input type="checkbox" id="notify_security" class="h-5 w-5 text-[#21A038] rounded border-[#CED4DA] focus:ring-[#21A038]" checked="">
                        </div>
                        <div>
                            <label for="notification_method" class="block text-sm font-medium text-[#212529] mb-1">Способ уведомлений</label>
                            <select id="notification_method" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                                <option>SMS и Email</option>
                                <option>Только SMS</option>
                                <option>Только Email</option>
                                <option>Push-уведомления</option>
                            </select>
                        </div>
                        <button class="w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Сохранить настройки уведомлений</button>
                    </div>
                </div>

                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Безопасность</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Управляйте паролем и дополнительными мерами безопасности.</p>
                    <div class="space-y-4">
                        <div>
                            <label for="current_password" class="block text-sm font-medium text-[#212529] mb-1">Текущий пароль</label>
                            <input type="password" id="current_password" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Введите текущий пароль">
                        </div>
                        <div>
                            <label for="new_password" class="block text-sm font-medium text-[#212529] mb-1">Новый пароль</label>
                            <input type="password" id="new_password" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Введите новый пароль">
                        </div>
                        <div>
                            <label for="confirm_password" class="block text-sm font-medium text-[#212529] mb-1">Подтвердите новый пароль</label>
                            <input type="password" id="confirm_password" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base" placeholder="Повторите новый пароль">
                        </div>
                        <button class="w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Изменить пароль</button>
                        <div class="flex items-center justify-between mt-6">
                            <label for="two_factor_auth" class="text-base text-[#212529]">Двухфакторная аутентификация</label>
                            <input type="checkbox" id="two_factor_auth" class="h-5 w-5 text-[#21A038] rounded border-[#CED4DA] focus:ring-[#21A038]" checked="">
                        </div>
                        <p class="text-xs text-[#6C757D] mt-1">Дополнительная защита вашего аккаунта.</p>
                    </div>
                </div>

                <div class="card">
                    <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-4">Язык и регион</h2>
                    <p class="text-sm md:text-base text-[#6C757D] mb-4">Выберите язык интерфейса и предпочитаемый регион.</p>
                    <div class="space-y-4">
                        <div>
                            <label for="language_select" class="block text-sm font-medium text-[#212529] mb-1">Язык интерфейса</label>
                            <select id="language_select" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                                <option>Русский</option>
                                <option>English</option>
                            </select>
                        </div>
                        <div>
                            <label for="region_select" class="block text-sm font-medium text-[#212529] mb-1">Регион</label>
                            <select id="region_select" class="w-full p-3 border border-[#CED4DA] rounded-lg focus:ring-[#21A038] focus:border-[#21A038] text-base">
                                <option>Москва</option>
                                <option>Санкт-Петербург</option>
                                <option>Екатеринбург</option>
                                <option>Другой</option>
                            </select>
                        </div>
                        <button class="w-full py-3 px-4 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Сохранить</button>
                    </div>
                </div>
            </div>
        </section>

        <div id="payment-confirm-modal" class="modal-overlay hidden">
            <div class="modal-content">
                <h2 class="text-xl md:text-2xl font-bold sber-malachite-text mb-4">Подтверждение платежа</h2>
                <p class="text-base md:text-lg text-[#212529] mb-4">Пожалуйста, проверьте детали платежа:</p>
                <div class="text-left bg-[#F8F9FA] p-4 rounded-md mb-6 space-y-2 text-sm">
                    <p><strong>Получатель:</strong> <span id="modal-recipient"></span></p>
                    <p><strong>Сумма:</strong> <span id="modal-amount"></span></p>
                    <p><strong>Назначение:</strong> <span id="modal-purpose"></span></p>
                    <p><strong>Со счета:</strong> <span id="modal-account-from"></span></p>
                </div>
                <p class="text-xs md:text-sm text-red-600 mb-4">Шаг 4: Подтвердите операцию кодом из SMS (имитация).</p>
                <div class="flex flex-col sm:flex-row justify-center space-y-3 sm:space-y-0 sm:space-x-4">
                    <button id="confirm-payment-button" class="py-2 px-6 bg-[#21A038] text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Подтвердить</button>
                    <button id="cancel-payment-button" class="py-2 px-6 bg-[#CED4DA] text-[#212529] rounded-lg font-semibold hover:bg-[#ADB5BD] transition-colors duration-200 text-base">Отмена</button>
                </div>
            </div>
        </div>

        <div id="payment-result-modal" class="modal-overlay hidden">
            <div class="modal-content">
                <h2 class="text-xl md:text-2xl font-bold sber-green-text mb-4">Платеж успешно отправлен!</h2>
                <p class="text-base md:text-lg text-[#212529] mb-4">Шаг 5: Дождитесь статуса "Выполнено". Обычно мгновенно или в течение рабочего дня.</p>
                <p class="text-xs md:text-sm text-[#6C757D] mb-6">Вы можете сохранить квитанцию в PDF или экспортировать в бухгалтерию.</p>
                <div class="flex flex-col sm:flex-row justify-center space-y-3 sm:space-y-0 sm:space-x-4">
                    <button class="py-2 px-6 sber-malachite-bg text-white rounded-lg font-semibold hover:bg-opacity-90 transition-colors duration-200 text-base">Скачать квитанцию (PDF)</button>
                    <button class="py-2 px-6 bg-[#E9ECEF] text-[#212529] rounded-lg font-semibold hover:bg-[#CED4DA] transition-colors duration-200 text-base" onclick="showPage(&#39;dashboard&#39;); document.getElementById(&#39;payment-result-modal&#39;).classList.add(&#39;hidden&#39;);">Вернуться на главную</button>
                </div>
            </div>
        </div>

        <div id="glossary-modal" class="modal-overlay hidden">
            <div class="modal-content max-w-2xl text-left">
                <h2 class="text-xl md:text-2xl font-bold sber-malachite-text mb-4 text-center">Глоссарий для предпринимателей</h2>
                <div class="overflow-y-auto max-h-96 pr-2">
                    <dl class="space-y-4">
                        <div>
                            <dt class="font-semibold text-lg text-[#212529]">ИП (Индивидуальный предприниматель)</dt>
                            <dd class="text-base text-[#6C757D]">Физическое лицо, зарегистрированное в установленном законом порядке и осуществляющее предпринимательскую деятельность без образования юридического лица.</dd>
                        </div>
                        <div>
                            <dt class="font-semibold text-lg text-[#212529]">ООО (Общество с ограниченной ответственностью)</dt>
                            <dd class="text-base text-[#6C757D]">Юридическое лицо, учрежденное одним или несколькими лицами, уставный капитал которого разделен на доли. Участники ООО несут риск убытков только в пределах стоимости своих долей.</dd>
                        </div>
                        <div>
                            <dt class="font-semibold text-lg text-[#212529]">Самозанятый (Налог на профессиональный доход)</dt>
                            <dd class="text-base text-[#6C757D]">Специальный налоговый режим для физических лиц и ИП, которые получают доход от своей деятельности, не имея работодателя и наемных работников.</dd>
                        </div>
                        <div>
                            <dt class="font-semibold text-lg text-[#212529]">РКО (Расчетно-кассовое обслуживание)</dt>
                            <dd class="text-base text-[#6C757D]">Комплекс банковских услуг по ведению счетов клиентов, осуществлению платежей, кассовых операций и других финансовых услуг.</dd>
                        </div>
                        <div>
                            <dt class="font-semibold text-lg text-[#212529]">Эквайринг</dt>
                            <dd class="text-base text-[#6C757D]">Услуга, предоставляемая банком (эквайером) по приему платежей с использованием банковских карт или других электронных средств оплаты (например, QR-кодов).</dd>
                        </div>
                        <div>
                            <dt class="font-semibold text-lg text-[#212529]">УСН (Упрощенная система налогообложения)</dt>
                            <dd class="text-base text-[#6C757D]">Один из специальных налоговых режимов, который позволяет малым и средним предприятиям снизить налоговую нагрузку и упростить ведение учета.</dd>
                        </div>
                    </dl>
                </div>
                <button class="btn-primary mt-6" onclick="this.closest(&#39;.modal-overlay&#39;).classList.add(&#39;hidden&#39;)">Закрыть</button>
            </div>
        </div>

        <div id="calendar-modal" class="modal-overlay hidden">
            <div class="modal-content max-w-2xl text-left">
                <h2 class="text-xl md:text-2xl font-bold sber-malachite-text mb-4 text-center">Календарь важных дат для бизнеса</h2>
                <div class="overflow-y-auto max-h-96 pr-2">
                    <h3 class="font-semibold text-lg text-[#212529] mb-2">Примеры важных дат (УСН 6%):</h3>
                    <ul class="list-disc list-inside space-y-2 text-base text-[#6C757D] mb-4">
                        <li>**25 января:** Срок уплаты авансового платежа по УСН за предыдущий квартал.</li>
                        <li>**25 марта:** Срок сдачи годовой декларации по УСН для организаций.</li>
                        <li>**25 апреля:** Срок сдачи годовой декларации по УСН для ИП.</li>
                        <li>**28 апреля:** Срок уплаты налога по УСН за предыдущий год.</li>
                        <li>**15 июля:** Срок уплаты страховых взносов ИП за предыдущий год в фиксированном размере.</li>
                        <li>**25 июля:** Срок уплаты авансового платежа по УСН за полугодие.</li>
                        <li>**25 октября:** Срок уплаты авансового платежа по УСН за 9 месяцев.</li>
                    </ul>
                    <p class="text-sm text-[#212529] font-medium">Совет: Эти даты могут меняться, всегда проверяйте актуальную информацию в личном кабинете ФНС или в разделе "Налоги и отчетность" в СберБизнес.Старт.</p>
                </div>
                <button class="btn-primary mt-6" onclick="this.closest(&#39;.modal-overlay&#39;).classList.add(&#39;hidden&#39;)">Закрыть</button>
            </div>
        </div>

        <button id="ai-assistant-button" class="ai-assistant-button">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-8 h-8 text-white">
                <text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" font-family="Inter, sans-serif" font-size="12" font-weight="bold" fill="white">AI</text>
            </svg>
        </button>

        <div id="ai-assistant-modal" class="ai-chat-modal hidden">
            <div class="ai-chat-window">
                <div class="chat-header">
                    <span>AI-ассистент ✨</span>
                    <button id="close-ai-chat" class="text-white text-xl leading-none">×</button>
                </div>
                <div id="chat-messages" class="chat-messages flex flex-col">
                    <div class="message-bubble message-ai">
                        Здравствуйте! Я ваш AI-ассистент. Чем могу помочь сегодня?
                    </div>
                </div>
                <div class="chat-input-area">
                    <input type="text" id="ai-chat-input" placeholder="Введите ваше сообщение...">
                    <button id="toggle-voice-input" class="bg-blue-500 text-white p-2 rounded-lg">🎤</button>
                    <button id="send-ai-message">Отправить</button>
                </div>
            </div>
        </div>
    </main>

    <script>
        // Updated Sberbank colors according to the guide
        const primaryColor = '#21A038'; // Sber Green (HEX: #21A038)
        const secondaryColor = '#107F8C'; // Malachite (HEX: #107F8C)
        const seaWaveColor = '#21A19A'; // Sea Wave (HEX: #21A19A)
        const cloverColor = '#31C2A7'; // Clover (HEX: #31C2A7)
        const darkTextColor = '#212529'; // Dark grey for main text
        const grayColor = '#6C757D'; // Grey for secondary text
        const lightGrayColor = '#CED4DA'; // Light grey for borders and element backgrounds
        const veryLightGrayColor = '#E9ECEF'; // Very light grey for table and button backgrounds

        // Function to wrap long labels for Chart.js (kept for compatibility if charts are added)
        function wrapLabels(labels, maxLength = 16) {
            return labels.map(label => {
                if (label.length <= maxLength) {
                    return label;
                }
                const words = label.split(' ');
                const lines = [];
                let currentLine = '';
                for (const word of words) {
                    if ((currentLine + word).length > maxLength && currentLine.length > 0) {
                        lines.push(currentLine.trim());
                        currentLine = '';
                    }
                    currentLine += word + ' ';
                }
                if (currentLine.length > 0) {
                    lines.push(currentLine.trim());
                }
                return lines;
            });
        }

        // Callback for Chart.js tooltip title (kept for compatibility)
        const tooltipTitleCallback = function(tooltipItems) {
            const item = tooltipItems[0];
            let label = item.chart.data.labels[item.dataIndex];
            if (Array.isArray(label)) {
              return label.join(' ');
            } else {
              return label;
            }
        };

        // Function to display a specific page and hide others
        function showPage(pageId) {
            document.querySelectorAll('.page-content').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId + '-page').classList.add('active');

            // Close mobile menu if open
            const mobileNavOverlay = document.getElementById('mobile-nav-overlay');
            if (!mobileNavOverlay.classList.contains('hidden')) {
                mobileNavOverlay.classList.add('hidden');
            }

            // Show/hide AI assistant button depending on the page
            const aiAssistantButton = document.getElementById('ai-assistant-button');
            const aiAssistantModal = document.getElementById('ai-assistant-modal');
            if (pageId === 'dashboard') {
                aiAssistantButton.classList.remove('hidden');
            } else {
                aiAssistantButton.classList.add('hidden');
                aiAssistantModal.classList.add('hidden'); // Hide modal if open
            }
        }

        // Event listeners for navigation links
        document.querySelectorAll('.nav-link').forEach(button => {
            button.addEventListener('click', () => {
                showPage(button.dataset.page);
                if (button.dataset.page === 'sberguide') {
                    sberGuide.showOverview(); // Show SberGuide overview when navigating to it
                } else if (button.dataset.page === 'support') {
                    support.showOverview(); // Show Support overview when navigating to it
                }
            });
        });

        // Toggle mobile menu
        document.getElementById('mobile-menu-button').addEventListener('click', () => {
            document.getElementById('mobile-nav-overlay').classList.remove('hidden');
        });
        document.getElementById('mobile-nav-overlay').addEventListener('click', (event) => {
            if (event.target === event.currentTarget) { // Close only when clicking on the overlay itself, not its content
                document.getElementById('mobile-nav-overlay').classList.add('hidden');
            }
        });

        // Payment process logic
        const submitPaymentButton = document.getElementById('submit-payment-button');
        const paymentConfirmModal = document.getElementById('payment-confirm-modal');
        const confirmPaymentButton = document.getElementById('confirm-payment-button');
        const cancelPaymentButton = document.getElementById('cancel-payment-button');
        const paymentResultModal = document.getElementById('payment-result-modal');

        submitPaymentButton.addEventListener('click', () => {
            const inn = document.getElementById('inn').value;
            const amount = document.getElementById('amount').value;
            const purpose = document.getElementById('purpose').value;
            const accountFrom = document.getElementById('account_from').value;

            if (!inn || !amount || !purpose || !accountFrom) {
                console.log('Пожалуйста, заполните все поля для платежа.');
                return;
            }

            // Populate modal with payment details
            document.getElementById('modal-recipient').textContent = `Поставщик (ИНН: ${inn})`;
            document.getElementById('modal-amount').textContent = `${amount} ₽`;
            document.getElementById('modal-purpose').textContent = purpose;
            document.getElementById('modal-account-from').textContent = accountFrom;

            paymentConfirmModal.classList.remove('hidden');
        });

        confirmPaymentButton.addEventListener('click', () => {
            paymentConfirmModal.classList.add('hidden');
            paymentResultModal.classList.remove('hidden');
            // Here you can add logic to simulate payment execution and update history
        });

        cancelPaymentButton.addEventListener('click', () => {
            paymentConfirmModal.classList.add('hidden');
        });

        // AI Assistant logic
        const aiAssistantButton = document.getElementById('ai-assistant-button');
        const aiAssistantModal = document.getElementById('ai-assistant-modal');
        const closeAiChatButton = document.getElementById('close-ai-chat');
        const chatMessagesContainer = document.getElementById('chat-messages');
        const aiChatInput = document.getElementById('ai-chat-input');
        const sendAiMessageButton = document.getElementById('send-ai-message');
        const toggleVoiceInputButton = document.getElementById('toggle-voice-input');

        let recognition;
        let isRecording = false;

        // Check for Web Speech API compatibility
        if ('webkitSpeechRecognition' in window) {
            recognition = new webkitSpeechRecognition();
            recognition.continuous = false; // Set to true for continuous recognition
            recognition.interimResults = false; // Get final results only
            recognition.lang = 'ru-RU'; // Set language to Russian

            recognition.onstart = () => {
                isRecording = true;
                toggleVoiceInputButton.textContent = '🔴 Запись...';
                toggleVoiceInputButton.classList.add('bg-red-500');
                toggleVoiceInputButton.classList.remove('bg-blue-500');
                console.log('Voice recognition started');
            };

            recognition.onresult = (event) => {
                const transcript = event.results[0][0].transcript;
                aiChatInput.value = transcript;
                sendMessage(); // Send the message after speech is recognized
            };

            recognition.onerror = (event) => {
                console.error('Speech recognition error:', event.error);
                isRecording = false;
                toggleVoiceInputButton.textContent = '🎤';
                toggleVoiceInputButton.classList.add('bg-blue-500');
                toggleVoiceInputButton.classList.remove('bg-red-500');
                addMessage('Ошибка голосового ввода. Попробуйте еще раз.', 'ai');
            };

            recognition.onend = () => {
                isRecording = false;
                toggleVoiceInputButton.textContent = '🎤';
                toggleVoiceInputButton.classList.add('bg-blue-500');
                toggleVoiceInputButton.classList.remove('bg-red-500');
                console.log('Voice recognition ended');
            };

            toggleVoiceInputButton.addEventListener('click', () => {
                if (isRecording) {
                    recognition.stop();
                } else {
                    recognition.start();
                }
            });
        } else {
            toggleVoiceInputButton.style.display = 'none'; // Hide button if not supported
            console.warn('Web Speech API not supported in this browser.');
        }


        aiAssistantButton.addEventListener('click', () => {
            aiAssistantModal.classList.remove('hidden');
        });

        closeAiChatButton.addEventListener('click', () => {
            aiAssistantModal.classList.add('hidden');
        });

        aiAssistantModal.addEventListener('click', (event) => {
            if (event.target === event.currentTarget) { // Close only when clicking on the overlay
                aiAssistantModal.classList.add('hidden');
            }
        });

        sendAiMessageButton.addEventListener('click', sendMessage);
        aiChatInput.addEventListener('keypress', (event) => {
            if (event.key === 'Enter') {
                sendMessage();
            }
        });

        function addMessage(text, sender) {
            const messageDiv = document.createElement('div');
            messageDiv.classList.add('message-bubble', sender === 'user' ? 'message-user' : 'message-ai');
            messageDiv.textContent = text;
            chatMessagesContainer.appendChild(messageDiv);
            chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight;
        }

        async function sendMessage() {
            const userMessage = aiChatInput.value.trim();
            if (userMessage === '') return;

            addMessage(userMessage, 'user');
            aiChatInput.value = '';

            // Add loading indicator
            const loadingMessageDiv = document.createElement('div');
            loadingMessageDiv.classList.add('message-bubble', 'message-ai', 'loading-dots');
            loadingMessageDiv.innerHTML = '<span>.</span><span>.</span><span>.</span>';
            chatMessagesContainer.appendChild(loadingMessageDiv);
            chatMessagesContainer.scrollTop = chatMessagesContainer.scrollHeight;

            try {
                // Prepare prompt for Gemini API
                const prompt = `Вы - AI-ассистент для платформы СберБизнес.Старт. Ваша задача - отвечать на вопросы пользователей, связанные с функциями платформы, финансами, налогами и ведением бизнеса. Также вы можете имитировать выполнение командных действий, если пользователь их запрашивает. Если вопрос не относится к этим темам, вежливо сообщите, что вы не можете на него ответить. Вот вопрос пользователя: "${userMessage}"

Примеры ответов:
- Если пользователь спрашивает про налоги: "Для оплаты налогов перейдите в раздел 'Платежи' и выберите 'Оплатить налоги'. Там вы сможете указать необходимые реквизиты."
- Если пользователь спрашивает про кредиты: "В разделе 'Продукты и Сервисы' вы найдете информацию о кредитах для бизнеса. Вы можете оформить заявку онлайн."
- Если пользователь говорит "Оплати счет": "Хорошо, для оплаты счета мне потребуется ИНН получателя, сумма и назначение платежа. Пожалуйста, предоставьте эти данные."
- Если пользователь спрашивает "сколько у меня осталось денег": "На ваших рублёвых счетах сейчас 30 478,62 ₽. Текущий баланс всех счетов составляет 1 250 000 ₽."
`;

                let chatHistory = [];
                chatHistory.push({ role: "user", parts: [{ text: prompt }] });

                const payload = { contents: chatHistory };
                const apiKey = ""; // Canvas will automatically provide the API key at runtime
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                const result = await response.json();

                // Remove loading indicator
                chatMessagesContainer.removeChild(loadingMessageDiv);

                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const aiResponse = result.candidates[0].content.parts[0].text;
                    addMessage(aiResponse, 'ai');
                } else {
                    addMessage("Извините, не удалось получить ответ от AI-ассистента. Пожалуйста, попробуйте еще раз.", 'ai');
                }
            } catch (error) {
                console.error('Ошибка при вызове Gemini API:', error);
                // Remove loading indicator in case of error
                if(chatMessagesContainer.contains(loadingMessageDiv)) {
                    chatMessagesContainer.removeChild(loadingMessageDiv);
                }
                addMessage("Произошла ошибка при обработке вашего запроса. Пожалуйста, проверьте ваше интернет-соединение или попробуйте позже.", 'ai');
            }
        }

        // SberGuide Logic (kept for other pages, but not directly on Dashboard)
        const sberGuide = {
            modules: [
                {
                    module_id: "mod_001",
                    module_title: "Регистрация бизнеса",
                    icon: "🚀",
                    description: "Основные шаги для регистрации бизнеса и открытия первого счета.",
                    steps: [
                        {
                            step_id: "mod_001_step_01",
                            type: "text_info",
                            title: "Формы регистрации бизнеса",
                            subtitle: "Шаг 1 из 4 — Выбор формы регистрации",
                            content: "Вы можете зарегистрироваться как ИП, самозанятый или ООО. Самозанятые — самый простой способ начать.",
                            cta: "Сравнить формы",
                            action: "show_comparison",
                            comparison_data: {
                                headers: ["Форма", "Плюсы", "Минусы"],
                                rows: [
                                    ["ИП", "Простота регистрации, меньше отчетности", "Ответственность личным имуществом"],
                                    ["Самозанятый", "Минимальные налоги, простое приложение", "Ограничения по доходу и видам деятельности"],
                                    ["ООО", "Разделение ответственности, больше возможностей", "Сложная регистрация, больше отчетности"]
                                ]
                            }
                        },
                        {
                            step_id: "mod_001_step_02",
                            type: "quiz",
                            title: "Микро-квиз",
                            subtitle: "Шаг 2 из 4 — Проверка знаний",
                            question: "Что из этого подходит для самозанятого?",
                            options: [
                                { label: "Открытие ООО", correct: false, feedback: "❌ Почти. Самозанятые используют спецприложение и не платят НДС." },
                                { label: "Переход на УСН", correct: false, feedback: "❌ Почти. Самозанятые используют спецприложение и не платят НДС." },
                                { label: "Регистрация через “Мой налог”", correct: true, feedback: "✅ Верно! Самозанятые регистрируются в “Мой налог” без бухгалтера." }
                            ]
                        },
                        {
                            step_id: "mod_001_step_03",
                            type: "checklist",
                            title: "Перед регистрацией подготовьте:",
                            subtitle: "Шаг 3 из 4 — Подготовка документов",
                            items: ["Паспорт", "Телефон с Госуслугами", "Карта Сбера (если нужна)"]
                        },
                        {
                            step_id: "mod_001_step_04",
                            type: "cta_action",
                            title: "Готовы зарегистрироваться?",
                            subtitle: "Шаг 4 из 4 — Действие",
                            text: "Нажмите кнопку, чтобы перейти к форме регистрации бизнеса.",
                            button: "Перейти к регистрации",
                            action: "external_redirect" // Simulates redirect
                        }
                    ]
                },
                {
                    module_id: "mod_002",
                    module_title: "Управление финансами",
                    icon: "💸",
                    description: "Как эффективно управлять доходами и расходами, совершать платежи.",
                    steps: [
                        {
                            step_id: "mod_002_step_01",
                            type: "text_info",
                            title: "Платежи и переводы",
                            subtitle: "Шаг 1 из 3 — Основы",
                            content: "Научитесь быстро и безопасно совершать платежи контрагентам и переводы внутри банка.",
                            cta: "Посмотреть видеоурок",
                            action: "show_video"
                        },
                        {
                            step_id: "mod_002_step_02",
                            type: "cta_action",
                            title: "Выставление счетов",
                            subtitle: "Шаг 2 из 3 — Практика",
                            text: "Создавайте и отправляйте счета своим клиентам прямо из приложения.",
                            button: "Выставить первый счёт",
                            action: "redirect_to_payments" // Simulates redirect to payments page
                        },
                        {
                            step_id: "mod_002_step_03",
                            type: "text_info",
                            title: "Анализ доходов и расходов",
                            subtitle: "Шаг 3 из 3 — Контроль",
                            content: "Используйте автоматическую категоризацию для понимания структуры ваших затрат.",
                            cta: "Перейти к аналитике",
                            action: "redirect_to_dashboard_expenses" // Simulates redirect
                        }
                    ]
                },
                {
                    module_id: "mod_003",
                    module_title: "Юридические аспекты и налоги",
                    icon: "⚖️",
                    description: "Основы налогообложения, отчетности и юридической безопасности.",
                    steps: [
                         {
                            step_id: "mod_003_step_01",
                            type: "text_info",
                            title: "Выбор системы налогообложения",
                            subtitle: "Шаг 1 из 3 — Важные решения",
                            content: "Узнайте о различных системах налогообложения (УСН, ОСНО) и выберите подходящую для вашего бизнеса. Правильный выбор поможет сэкономить.",
                            cta: "Сравнить системы",
                            action: "show_tax_comparison"
                        },
                        {
                            step_id: "mod_003_step_02",
                            type: "text_info",
                            title: "Сдача отчетности: сроки и формы",
                            subtitle: "Шаг 2 из 3 — Обязательства",
                            content: "Будьте в курсе всех сроков сдачи отчетности и необходимых форм, чтобы избежать штрафов. СберБизнес напомнит вам о важных датах.",
                            cta: "Посмотреть календарь",
                            action: "show_calendar"
                        },
                        {
                            step_id: "mod_003_step_03",
                            type: "cta_action",
                            title: "Юридическая поддержка",
                            subtitle: "Шаг 3 из 3 — Защита бизнеса",
                            text: "Получите квалифицированную юридическую помощь по любым вопросам, связанным с вашим бизнесом.",
                            button: "Получить консультацию",
                            action: "redirect_to_support"
                        }
                    ]
                },
                {
                    module_id: "mod_004",
                    module_title: "Планирование бюджета",
                    icon: "📊",
                    description: "Инструменты для роста вашего бизнеса и привлечения клиентов.",
                    steps: [
                        {
                            step_id: "mod_004_step_01",
                            type: "text_info",
                            title: "Основы бюджетирования",
                            subtitle: "Шаг 1 из 3 — Фундамент",
                            content: "Узнайте, как составить эффективный бюджет для вашего бизнеса, чтобы контролировать финансы и планировать развитие.",
                            cta: "Скачать шаблон",
                            action: "download_template"
                        },
                        {
                            step_id: "mod_004_step_02",
                            type: "cta_action",
                            title: "Установка лимитов расходов",
                            subtitle: "Шаг 2 из 3 — Контроль",
                            text: "Установите лимиты на расходы по категориям, чтобы избежать перерасхода и оптимизировать затраты.",
                            button: "Настроить лимиты",
                            action: "redirect_to_settings_expenses"
                        },
                        {
                            step_id: "mod_004_step_03",
                            type: "text_info",
                            title: "Прогноз денежных потоков",
                            subtitle: "Шаг 3 из 3 — Прогнозирование",
                            content: "Научитесь прогнозировать будущие доходы и расходы, чтобы избежать кассовых разрывов и принимать обоснованные решения.",
                            cta: "Подробнее о прогнозе",
                            action: "redirect_to_dashboard_analytics"
                        }
                    ]
                },
                {
                    module_id: "mod_005",
                    module_title: "Проверка контрагентов",
                    icon: "🕵️",
                    description: "Где найти ответы на вопросы и поддержку от экспертов и коллег.",
                    steps: [
                        {
                            step_id: "mod_005_step_01",
                            type: "text_info",
                            title: "Зачем проверять контрагентов?",
                            subtitle: "Шаг 1 из 3 — Безопасность",
                            content: "Проверка контрагентов помогает избежать рисков, связанных с недобросовестными партнерами, и защитить ваш бизнес.",
                            cta: "Посмотреть кейсы",
                            action: "show_cases"
                        },
                        {
                            step_id: "mod_005_step_02",
                            type: "cta_action",
                            title: "Как проверить контрагента",
                            subtitle: "Шаг 2 из 3 — Инструменты",
                            text: "Используйте встроенные инструменты СберБизнес для быстрой и надежной проверки.",
                            button: "Проверить контрагента",
                            action: "redirect_to_payments_check"
                        },
                        {
                            step_id: "mod_005_step_03",
                            type: "text_info",
                            title: "Важность благонадежности",
                            subtitle: "Шаг 3 из 3 — Доверие",
                            content: "Сотрудничество только с проверенными партнерами — залог стабильности и успеха вашего бизнеса.",
                            cta: "Узнать больше",
                            action: "read_more"
                        }
                    ]
                }
            ],
            user_context: {
                registered: null, // true/false
                form: null, // 'ИП', 'Самозанятый', 'ООО', 'Пока нет'
                experience: null // 'Новичок', 'Пользовался другими', 'Опытный'
            },
            user_learning_state: {
                currentModuleId: null,
                currentStepIndex: -1,
                completedModules: {}, // { moduleId: true }
                badges: []
            },

            init: function() {
                this.loadState();
                this.renderModuleOverview();
                this.updateProgressBar();

                // Event listeners for navigation within SberGuide
                document.getElementById('back-to-modules').addEventListener('click', () => this.showOverview());
                document.getElementById('next-step').addEventListener('click', () => this.nextStep());
                document.getElementById('previous-step').addEventListener('click', () => this.previousStep());
                document.getElementById('apply-now-button').addEventListener('click', () => this.handleCtaAction());
                document.getElementById('complete-module-button').addEventListener('click', () => this.completeModule());
                document.getElementById('go-to-next-module').addEventListener('click', () => this.goToNextModule());

                // Initial onboarding prompt (simulated)
                if (!this.user_context.registered && !this.user_context.form && !this.user_context.experience) {
                    this.showOnboardingPrompt();
                }
            },

            loadState: function() {
                const savedContext = localStorage.getItem('sberGuideUserContext');
                const savedState = localStorage.getItem('sberGuideUserLearningState');
                if (savedContext) {
                    this.user_context = JSON.parse(savedContext);
                }
                if (savedState) {
                    this.user_learning_state = JSON.parse(savedState);
                }
            },

            saveState: function() {
                localStorage.setItem('sberGuideUserContext', JSON.stringify(this.user_context));
                localStorage.setItem('sberGuideUserLearningState', JSON.stringify(this.user_learning_state));
            },

            showOnboardingPrompt: function() {
                // This would be a modal or a dedicated onboarding flow
                console.log("Showing onboarding prompt for SberGuide...");
                // For simplicity, let's set some default context for demo
                if (!this.user_context.experience) {
                    this.user_context.experience = 'Новичок';
                    this.saveState();
                    this.updateProgressBar(); // Update progress bar after setting context
                }
            },

            updateProgressBar: function() {
                const totalModules = this.modules.length;
                const completedCount = Object.keys(this.user_learning_state.completedModules).length;
                const progressPercentage = (completedCount / totalModules) * 100;

                document.getElementById('sberguide-progress-bar').style.width = `${progressPercentage}%`;
                document.getElementById('sberguide-progress-text').innerText = `${progressPercentage.toFixed(0)}% пройдено (${completedCount} из ${totalModules} модулей)`;

                this.renderModuleList(); // Re-render modules to update button states
            },

            renderModuleList: function() {
                const modulesListDiv = document.getElementById('sberguide-modules-list');
                modulesListDiv.innerHTML = ''; // Clear previous modules

                this.modules.forEach(module => {
                    const isCompleted = this.user_learning_state.completedModules[module.module_id];
                    const moduleCard = document.createElement('div');
                    moduleCard.classList.add('card');
                    moduleCard.innerHTML = `
                        <div class="sber-green-text icon-large mb-3">${module.icon}</div>
                        <h2 class="text-xl md:text-2xl font-semibold sber-malachite-text mb-3">${module.module_title}</h2>
                        <p class="text-sm md:text-base text-[#6C757D] mb-4">${module.description}</p>
                        <button class="w-full py-2 px-4 ${isCompleted ? 'sber-malachite-bg' : 'bg-[#21A038]'} text-white rounded-lg font-semibold hover:opacity-90 transition-colors duration-200 text-base"
                                onclick="sberGuide.startModule('${module.module_id}')">
                            ${isCompleted ? '🔁 Повторить' : (this.user_learning_state.currentModuleId === module.module_id ? '▶ Продолжить' : '▶ Начать')}
                        </button>
                    `;
                    modulesListDiv.appendChild(moduleCard);
                });
            },

            showOverview: function() {
                document.getElementById('sberguide-overview-screen').classList.remove('hidden');
                document.getElementById('sberguide-learning-screen').classList.add('hidden');
                document.getElementById('sberguide-completion-screen').classList.add('hidden');
                this.user_learning_state.currentModuleId = null;
                this.user_learning_state.currentStepIndex = -1;
                this.saveState();
                this.updateProgressBar();
            },

            startModule: function(moduleId) {
                this.user_learning_state.currentModuleId = moduleId;
                // If module is completed, start from beginning, otherwise resume
                if (this.user_learning_state.completedModules[moduleId]) {
                    this.user_learning_state.currentStepIndex = 0;
                } else if (this.user_learning_state.currentModuleId === moduleId && this.user_learning_state.currentStepIndex !== -1) {
                    // Continue from where left off
                } else {
                    this.user_learning_state.currentStepIndex = 0;
                }
                this.saveState();
                this.showLearningScreen();
            },

            showLearningScreen: function() {
                document.getElementById('sberguide-overview-screen').classList.add('hidden');
                document.getElementById('sberguide-learning-screen').classList.remove('hidden');
                document.getElementById('sberguide-completion-screen').classList.add('hidden');
                this.renderCurrentStep();
            },

            renderCurrentStep: function() {
                const currentModule = this.modules.find(m => m.module_id === this.user_learning_state.currentModuleId);
                if (!currentModule) {
                    console.error("Current module not found!");
                    this.showOverview();
                    return;
                }

                const currentStep = currentModule.steps[this.user_learning_state.currentStepIndex];
                if (!currentStep) {
                    this.completeModule();
                    return;
                }

                document.getElementById('learning-module-title').innerText = currentModule.module_title;
                document.getElementById('learning-step-subtitle').innerText = currentStep.subtitle;
                const contentDiv = document.getElementById('learning-step-content');
                contentDiv.innerHTML = ''; // Clear previous content

                // Hide all action buttons by default
                document.getElementById('next-step').classList.add('hidden');
                document.getElementById('previous-step').classList.add('hidden');
                document.getElementById('apply-now-button').classList.add('hidden');
                document.getElementById('complete-module-button').classList.add('hidden');

                switch (currentStep.type) {
                    case 'text_info':
                        contentDiv.innerHTML = `<p class="text-base text-[#212529]">${currentStep.content}</p>`;
                        if (currentStep.cta) {
                            const ctaButton = document.createElement('button');
                            ctaButton.classList.add('btn-secondary', 'mt-4');
                            ctaButton.innerText = currentStep.cta;
                            ctaButton.onclick = () => this.handleCtaAction(currentStep.action, currentStep.comparison_data);
                            contentDiv.appendChild(ctaButton);
                        }
                        document.getElementById('next-step').classList.remove('hidden');
                        break;
                    case 'quiz':
                        contentDiv.innerHTML = `
                            <p class="text-base text-[#212529] font-semibold mb-3">${currentStep.question}</p>
                            <div id="quiz-options"></div>
                            <div id="quiz-feedback" class="quiz-feedback hidden"></div>
                            <button id="submit-quiz" class="btn-primary mt-4">Проверить ответ</button>
                        `;
                        const quizOptionsDiv = document.getElementById('quiz-options');
                        currentStep.options.forEach((option, index) => {
                            const optionDiv = document.createElement('div');
                            optionDiv.classList.add('quiz-option');
                            optionDiv.innerText = option.label;
                            optionDiv.dataset.index = index;
                            optionDiv.addEventListener('click', (e) => {
                                document.querySelectorAll('.quiz-option').forEach(opt => opt.classList.remove('selected'));
                                e.target.classList.add('selected');
                            });
                            quizOptionsDiv.appendChild(optionDiv);
                        });
                        document.getElementById('submit-quiz').addEventListener('click', () => this.submitQuiz(currentStep));
                        break;
                    case 'checklist':
                        contentDiv.innerHTML = `
                            <p class="text-base text-[#212529] font-semibold mb-3">${currentStep.title}</p>
                            <div id="checklist-items"></div>
                            <button id="complete-checklist" class="btn-primary mt-4">✅ Все готово</button>
                        `;
                        const checklistItemsDiv = document.getElementById('checklist-items');
                        currentStep.items.forEach((item, index) => {
                            const itemDiv = document.createElement('div');
                            itemDiv.classList.add('checklist-item');
                            itemDiv.innerHTML = `
                                <input type="checkbox" id="checklist-item-${index}">
                                <label for="checklist-item-${index}" class="text-base text-[#212529]">${item}</label>
                            `;
                            checklistItemsDiv.appendChild(itemDiv);
                        });
                        document.getElementById('complete-checklist').addEventListener('click', () => this.completeChecklist(currentStep));
                        break;
                    case 'cta_action':
                        contentDiv.innerHTML = `
                            <p class="text-base text-[#212529]">${currentStep.text}</p>
                        `;
                        document.getElementById('apply-now-button').innerText = currentStep.button;
                        document.getElementById('apply-now-button').dataset.action = currentStep.action;
                        document.getElementById('apply-now-button').classList.remove('hidden');
                        document.getElementById('next-step').classList.remove('hidden'); // Allow to skip CTA if needed
                        break;
                }

                if (this.user_learning_state.currentStepIndex > 0) {
                    document.getElementById('previous-step').classList.remove('hidden');
                }

                const totalSteps = currentModule.steps.length;
                document.getElementById('learning-footer-progress').innerText = `🏁 До конца модуля — ${totalSteps - (this.user_learning_state.currentStepIndex + 1)} шага`;
                if (this.user_learning_state.currentStepIndex === totalSteps - 1) {
                    document.getElementById('next-step').classList.add('hidden');
                    document.getElementById('complete-module-button').classList.remove('hidden');
                }
            },

            nextStep: function() {
                const currentModule = this.modules.find(m => m.module_id === this.user_learning_state.currentModuleId);
                if (this.user_learning_state.currentStepIndex < currentModule.steps.length - 1) {
                    this.user_learning_state.currentStepIndex++;
                    this.saveState();
                    this.renderCurrentStep();
                } else {
                    this.completeModule();
                }
            },

            previousStep: function() {
                if (this.user_learning_state.currentStepIndex > 0) {
                    this.user_learning_state.currentStepIndex--;
                    this.saveState();
                    this.renderCurrentStep();
                }
            },

            submitQuiz: function(step) {
                const selectedOption = document.querySelector('.quiz-option.selected');
                const feedbackDiv = document.getElementById('quiz-feedback');
                feedbackDiv.classList.remove('hidden', 'correct', 'incorrect');

                if (selectedOption) {
                    const selectedIndex = parseInt(selectedOption.dataset.index);
                    const isCorrect = step.options[selectedIndex].correct;
                    feedbackDiv.innerText = step.options[selectedIndex].feedback;
                    if (isCorrect) {
                        feedbackDiv.classList.add('correct');
                        document.getElementById('submit-quiz').disabled = true; // Disable after correct answer
                        document.getElementById('next-step').classList.remove('hidden'); // Enable next step
                    } else {
                        feedbackDiv.classList.add('incorrect');
                    }
                } else {
                    feedbackDiv.innerText = "Пожалуйста, выберите ответ.";
                    feedbackDiv.classList.add('incorrect');
                }
            },

            completeChecklist: function(step) {
                const allChecked = Array.from(document.querySelectorAll('#checklist-items input[type="checkbox"]')).every(checkbox => checkbox.checked);
                if (allChecked) {
                    console.log("Checklist completed!");
                    document.getElementById('complete-checklist').disabled = true;
                    document.getElementById('next-step').classList.remove('hidden'); // Enable next step
                } else {
                    console.log("Please check all items.");
                    // Optionally, show a message to the user
                }
            },

            handleCtaAction: function(actionType, data) {
                console.log(`Performing CTA action: ${actionType}`);
                switch (actionType) {
                    case 'show_comparison':
                        this.showComparisonModal(data);
                        break;
                    case 'external_redirect':
                        // Simulate external redirect
                        console.log("Simulating redirect to registration form.");
                        // window.open('https://example.com/registration', '_blank');
                        break;
                    case 'redirect_to_payments':
                        showPage('payments');
                        break;
                    case 'redirect_to_dashboard_expenses':
                        showPage('dashboard'); // Assuming dashboard shows expenses
                        break;
                    case 'show_video':
                        console.log("Simulating video playback.");
                        // Open a modal with a video player
                        break;
                    case 'show_tax_comparison':
                         this.showComparisonModal({
                            headers: ["Система", "Ставка", "Особенности"],
                            rows: [
                                ["УСН 6%", "6% от доходов", "Простота, подходит для услуг"],
                                ["ОСНО", "НДС, НДФЛ, налог на прибыль", "Сложно, для крупного бизнеса"],
                                ["НПД", "4-6% от дохода", "Для самозанятых, до 2.4 млн ₽/год"]
                            ]
                        });
                        break;
                    case 'show_calendar':
                        this.showCalendarModal();
                        break;
                    case 'redirect_to_support':
                        showPage('support');
                        break;
                    case 'download_template':
                        console.log("Simulating template download.");
                        // Trigger a file download
                        break;
                    case 'redirect_to_settings_expenses':
                        showPage('settings'); // Assuming settings has expense limits
                        break;
                    case 'redirect_to_dashboard_analytics':
                        showPage('dashboard'); // Assuming dashboard has analytics
                        break;
                    case 'show_cases':
                        console.log("Simulating case studies display.");
                        // Show a modal with case studies
                        break;
                    case 'redirect_to_payments_check':
                        showPage('payments'); // Assuming payments has a counterparty check
                        break;
                    case 'read_more':
                        console.log("Simulating 'read more' action.");
                        // Open a new page or modal with more info
                        break;
                }
            },

            showComparisonModal: function(data) {
                const modalOverlay = document.createElement('div');
                modalOverlay.classList.add('modal-overlay');
                modalOverlay.innerHTML = `
                    <div class="modal-content">
                        <h3 class="text-xl font-bold sber-malachite-text mb-4">Сравнение</h3>
                        <div class="overflow-x-auto mb-4">
                            <table class="min-w-full divide-y divide-[#CED4DA] rounded-lg">
                                <thead class="bg-[#E9ECEF]">
                                    <tr>
                                        ${data.headers.map(h => `<th class="px-4 py-2 text-left text-xs font-medium text-[#6C757D] uppercase tracking-wider">${h}</th>`).join('')}
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-[#CED4DA)">
                                    ${data.rows.map(row => `
                                        <tr>
                                            ${row.map(cell => `<td class="px-4 py-2 whitespace-nowrap text-sm text-[#212529]">${cell}</td>`).join('')}
                                        </tr>
                                    `).join('')}
                                </tbody>
                            </table>
                        </div>
                        <button class="btn-primary" onclick="this.closest('.modal-overlay').remove()">Закрыть</button>
                    </div>
                `;
                document.body.appendChild(modalOverlay);
            },

            completeModule: function() {
                const currentModuleId = this.user_learning_state.currentModuleId;
                const currentModule = this.modules.find(m => m.module_id === currentModuleId);

                if (currentModule && !this.user_learning_state.completedModules[currentModuleId]) {
                    this.user_learning_state.completedModules[currentModuleId] = true;
                    this.user_learning_state.badges.push(`🏅 ${currentModule.module_title} — освоено`);
                    this.saveState();
                    this.updateProgressBar();

                    document.getElementById('sberguide-learning-screen').classList.add('hidden');
                    document.getElementById('sberguide-completion-screen').classList.remove('hidden');
                    document.getElementById('completed-module-badge').innerText = `🏅 ${currentModule.module_title} — освоено`;

                    // Check if there's a next module
                    const currentIndex = this.modules.findIndex(m => m.module_id === currentModuleId);
                    if (currentIndex < this.modules.length - 1) {
                        document.getElementById('go-to-next-module').classList.remove('hidden');
                        document.getElementById('go-to-next-module').dataset.nextModuleId = this.modules[currentIndex + 1].module_id;
                    } else {
                        document.getElementById('go-to-next-module').classList.add('hidden');
                    }
                } else {
                    this.showOverview(); // If already completed or error, go back to overview
                }
            },

            goToNextModule: function() {
                const nextModuleId = document.getElementById('go-to-next-module').dataset.nextModuleId;
                if (nextModuleId) {
                    this.startModule(nextModuleId);
                } else {
                    this.showOverview();
                }
            },

            // New SberGuide Glossary Modal
            showGlossaryModal: function() {
                document.getElementById('glossary-modal').classList.remove('hidden');
            },

            // New SberGuide Calendar Modal
            showCalendarModal: function() {
                document.getElementById('calendar-modal').classList.remove('hidden');
            }
        };

        // Knowledge Base Logic
        const support = {
            knowledgeBase: {
                start: {
                    title: "Начало работы в СберБизнес.Старт",
                    content: `
                        <p>Добро пожаловать в СберБизнес.Старт! Этот раздел поможет вам быстро освоиться и начать работу.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">1. Регистрация и первый вход</h3>
                        <p>Если вы еще не зарегистрированы, пройдите простую процедуру регистрации на нашем сайте. После успешной регистрации вы получите логин и пароль для входа в личный кабинет.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">2. Обзор главного экрана</h3>
                        <p>На главном экране "Мой Бизнес" вы увидите ключевые финансовые показатели: текущий баланс, доходы и расходы. Также здесь расположены кнопки для быстрых действий, таких как "Оплатить счет" или "Выставить счет".</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">3. Персонализация</h3>
                        <p>В разделе "Настройки" вы можете персонализировать уведомления, язык приложения и другие параметры, чтобы сделать работу максимально удобной для вас.</p>
                        <p class="text-sm text-[#6C757D] mt-4">Совет: Рекомендуем пройти первый модуль "Регистрация бизнеса" в СберГайде для полного понимания основ.</p>
                    `
                },
                payments: {
                    title: "Платежи и переводы: пошаговое руководство",
                    content: `
                        <p>Осуществление платежей и переводов — одна из основных операций в вашем бизнесе. Мы сделали этот процесс максимально простым.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">1. Создание нового платежа</h3>
                        <p>Перейдите в раздел "Платежи" и нажмите "Создать новый платеж". Вам потребуется ввести ИНН или название компании-получателя. Система автоматически подтянет остальные реквизиты.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">2. Указание суммы и назначения</h3>
                        <p>Введите сумму платежа и максимально подробно опишите его назначение. Это важно для корректного учета и налоговой отчетности.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">3. Использование шаблонов</h3>
                        <p>Для часто повторяющихся платежей создавайте шаблоны. Это сэкономит ваше время и снизит вероятность ошибок при вводе реквизитов.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">4. Проверка и подтверждение</h3>
                        <p>Перед отправкой платежа внимательно проверьте все данные. Подтвердите операцию с помощью кода из SMS или другим способом, указанным в настройках безопасности.</p>
                        <p class="text-sm text-[#6C757D] mt-4">Совет: Всегда сохраняйте квитанции об оплате для вашего бухгалтерского учета.</p>
                    `
                },
                taxes: {
                    title: "Налоги и отчетность: что нужно знать молодому предпринимателю",
                    content: `
                        <p>Налогообложение — важная часть ведения бизнеса. СберБизнес.Старт поможет вам разобраться в основных моментах.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">1. Выбор системы налогообложения</h3>
                        <p>В России существуют различные системы налогообложения (УСН, ОСНО, НПД). Выбор зависит от вида вашей деятельности, оборота и количества сотрудников. Наиболее популярной для малого бизнеса является УСН.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">2. СберКопилка для Налогов</h3>
                        <p>Используйте нашу СберКопилку для Налогов, чтобы автоматически резервировать процент от ваших доходов. Это поможет избежать проблем с уплатой налогов в срок.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">3. Сроки сдачи отчетности</h3>
                        <p>Следите за календарем важных дат, чтобы не пропустить сроки сдачи налоговых деклараций и уплаты взносов. В СберБизнес.Старт есть напоминания об этом.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">4. Онлайн-бухгалтерия</h3>
                        <p>Для упрощения ведения учета и формирования отчетности вы можете подключить онлайн-бухгалтерию через наш Маркетплейс.</p>
                        <p class="text-sm text-[#6C757D] mt-4">Совет: При возникновении вопросов по налогам всегда обращайтесь к квалифицированным специалистам или в службу поддержки.</p>
                    `
                },
                popular: {
                    title: "Популярные вопросы и ответы",
                    content: `
                        <p>Здесь собраны ответы на самые частые вопросы, которые возникают у наших пользователей.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">Как изменить реквизиты компании?</h3>
                        <p>Для изменения реквизитов вашей компании перейдите в раздел "Профиль бизнеса" в "Настройках" или свяжитесь с нашей службой поддержки.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">Что делать, если платеж не прошел?</h3>
                        <p>Проверьте статус платежа в "Истории платежей". Если статус "В обработке" более 1 рабочего дня или "Отклонен", обратитесь в чат с поддержкой, предоставив номер платежного поручения.</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">Как получить выписку по счету?</h3>
                        <p>Выписку по счету можно сформировать и скачать в разделе "Счета". Выберите нужный счет, период и формат файла (PDF или CSV).</p>
                        <h3 class="font-semibold text-lg text-[#212529] mt-4 mb-2">Как подключить эквайринг?</h3>
                        <p>Для подключения эквайринга перейдите в раздел "Продукты и Сервисы" и выберите "Эквайринг". Заполните заявку, и наш менеджер свяжется с вами.</p>
                        <p class="text-sm text-[#6C757D] mt-4">Если вы не нашли ответ на свой вопрос, воспользуйтесь поиском по Базе знаний или обратитесь в чат поддержки.</p>
                    `
                }
            },

            init: function() {
                document.querySelectorAll('.knowledge-category-link').forEach(button => {
                    button.addEventListener('click', (event) => {
                        const category = event.target.dataset.category;
                        this.showKnowledgeDetail(category);
                    });
                });
                document.getElementById('back-to-support-overview').addEventListener('click', () => this.showOverview());
            },

            showOverview: function() {
                document.getElementById('support-overview-screen').classList.remove('hidden');
                document.getElementById('knowledge-base-detail-screen').classList.add('hidden');
            },

            showKnowledgeDetail: function(category) {
                const data = this.knowledgeBase[category];
                if (data) {
                    document.getElementById('kb-detail-title').innerText = data.title;
                    document.getElementById('kb-detail-content').innerHTML = data.content;
                    document.getElementById('support-overview-screen').classList.add('hidden');
                    document.getElementById('knowledge-base-detail-screen').classList.remove('hidden');
                } else {
                    console.error("Knowledge base category not found:", category);
                }
            }
        };

        // Chart for Market Pulse Seasonality
        function createMarketSeasonalityChart() {
            const ctx = document.getElementById('marketSeasonalityChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: {
                    labels: ['Янв', 'Фев', 'Мар', 'Апр', 'Май', 'Июн', 'Июл', 'Авг', 'Сен', 'Окт', 'Ноя', 'Дек'],
                    datasets: [{
                        label: 'Сезонность спроса',
                        data: [70, 65, 80, 90, 85, 75, 60, 70, 95, 100, 90, 80],
                        borderColor: primaryColor,
                        backgroundColor: 'rgba(33, 160, 56, 0.1)',
                        fill: true,
                        tension: 0.3
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: {
                                callback: function(value) {
                                    return value + '%';
                                }
                            }
                        }
                    },
                    plugins: {
                        legend: { display: false },
                        tooltip: { callbacks: { title: tooltipTitleCallback } }
                    }
                }
            });
        }


        // Initialisation on DOMContentLoaded
        document.addEventListener('DOMContentLoaded', () => {
            showPage('dashboard'); // Start on the dashboard page
            sberGuide.init(); // Initialize SberGuide
            support.init(); // Initialize Support
            createMarketSeasonalityChart(); // Create the chart for Market Pulse
        });
    </script>


</body></html>
