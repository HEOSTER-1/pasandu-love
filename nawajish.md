<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <title>Unseen Love - 3D Cartoon Animation</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Comic Sans MS', 'Arial Black', cursive, sans-serif;
            overflow: hidden;
            background: #1a1a2e;
            color: #fff;
            perspective: 1000px;
            position: fixed;
            width: 100%;
            height: 100%;
        }

        #animation-container {
            width: 100vw;
            height: 100vh;
            position: relative;
            overflow: hidden;
        }

        .scene {
            position: absolute;
            width: 100%;
            height: 100%;
            opacity: 0;
            transition: opacity 1.5s ease-in-out;
            display: flex;
            align-items: center;
            justify-content: center;
            transform-style: preserve-3d;
        }

        .scene.active {
            opacity: 1;
            z-index: 1;
        }

        /* Scene Titles - Responsive */
        .scene-title {
            position: absolute;
            top: 3%;
            left: 50%;
            transform: translateX(-50%);
            font-size: clamp(1.2rem, 5vw, 3rem);
            font-weight: 900;
            text-align: center;
            background: linear-gradient(135deg, #ff6b9d 0%, #c44569 100%);
            padding: clamp(10px, 2vh, 25px) clamp(20px, 5vw, 60px);
            border-radius: 15px;
            z-index: 100;
            animation: title3D 2s ease-in;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.3);
            border: 3px solid #fff;
            box-shadow: 0 5px 20px rgba(0,0,0,0.5);
            max-width: 90%;
            line-height: 1.2;
        }

        .scene-description {
            position: absolute;
            bottom: 8%;
            left: 50%;
            transform: translateX(-50%);
            font-size: clamp(0.8rem, 3vw, 1.6rem);
            text-align: center;
            background: rgba(0,0,0,0.85);
            padding: clamp(10px, 2vh, 20px) clamp(15px, 4vw, 50px);
            border-radius: 15px;
            z-index: 100;
            max-width: 90%;
            line-height: 1.5;
            animation: desc3D 2s ease-in 0.5s backwards;
            border: 2px solid #fff;
            box-shadow: 0 5px 20px rgba(0,0,0,0.6);
        }

        @keyframes title3D {
            0% { opacity: 0; transform: translateX(-50%) scale(0.5); }
            100% { opacity: 1; transform: translateX(-50%) scale(1); }
        }

        @keyframes desc3D {
            0% { opacity: 0; transform: translateX(-50%) translateY(20px); }
            100% { opacity: 1; transform: translateX(-50%) translateY(0); }
        }

        /* Start Screen */
        #start-screen {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            flex-direction: column;
            z-index: 100;
            padding: 20px;
        }

        #start-screen h1 {
            font-size: clamp(2.5rem, 10vw, 6rem);
            margin-bottom: clamp(1rem, 3vh, 2rem);
            text-shadow: 4px 4px 0px rgba(0,0,0,0.3);
            animation: bounceIn 1.5s ease-in;
        }

        #start-screen p {
            font-size: clamp(1rem, 4vw, 2rem);
            margin-bottom: clamp(0.5rem, 2vh, 1rem);
            opacity: 0.95;
        }

        #start-btn {
            padding: clamp(15px, 3vh, 25px) clamp(30px, 8vw, 70px);
            font-size: clamp(1.2rem, 4vw, 2rem);
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            border: 3px solid white;
            color: white;
            cursor: pointer;
            border-radius: 50px;
            transition: all 0.3s;
            margin-top: clamp(15px, 3vh, 30px);
            font-weight: 900;
            box-shadow: 0 10px 30px rgba(0,0,0,0.4);
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
            touch-action: manipulation;
        }

        #start-btn:active {
            transform: scale(0.95);
        }

        @keyframes bounceIn {
            0% { transform: scale(0); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        /* ===== RESPONSIVE 3D CARTOON CHARACTERS ===== */
        
        /* 3D Cartoon Girl - Responsive */
        .cartoon-girl {
            position: relative;
            width: clamp(80px, 15vw, 140px);
            height: clamp(120px, 22vw, 200px);
            transform-style: preserve-3d;
            filter: drop-shadow(5px 5px 10px rgba(0,0,0,0.4));
        }

        .cartoon-girl .head {
            width: clamp(40px, 8vw, 70px);
            height: clamp(40px, 8vw, 70px);
            background: linear-gradient(135deg, #ffcdd2 0%, #ef9a9a 100%);
            border-radius: 50%;
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            border: clamp(3px, 0.5vw, 5px) solid #e91e63;
            box-shadow: inset -3px -3px 10px rgba(0,0,0,0.2),
                        0 5px 15px rgba(0,0,0,0.3);
        }

        .cartoon-girl .hair {
            width: clamp(45px, 9vw, 80px);
            height: clamp(30px, 6vw, 50px);
            background: linear-gradient(135deg, #5d4037 0%, #3e2723 100%);
            border-radius: 50% 50% 0 0;
            position: absolute;
            top: clamp(-15px, -2vw, -25px);
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-girl .ponytail {
            width: clamp(18px, 3vw, 30px);
            height: clamp(25px, 4vw, 40px);
            background: linear-gradient(135deg, #5d4037 0%, #3e2723 100%);
            border-radius: 50%;
            position: absolute;
            top: clamp(-10px, -1.5vw, -15px);
            right: clamp(-15px, -2.5vw, -25px);
            transform: rotate(-20deg);
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-girl .eye-left,
        .cartoon-girl .eye-right {
            width: clamp(8px, 1.5vw, 14px);
            height: clamp(8px, 1.5vw, 14px);
            background: #000;
            border-radius: 50%;
            position: absolute;
            top: clamp(15px, 3vw, 25px);
        }

        .cartoon-girl .eye-left { left: clamp(10px, 2vw, 18px); }
        .cartoon-girl .eye-right { right: clamp(10px, 2vw, 18px); }

        .cartoon-girl .eye-left::after,
        .cartoon-girl .eye-right::after {
            content: '';
            width: clamp(3px, 0.6vw, 6px);
            height: clamp(3px, 0.6vw, 6px);
            background: white;
            border-radius: 50%;
            position: absolute;
            top: 2px;
            left: 2px;
        }

        .cartoon-girl .smile {
            width: clamp(18px, 3vw, 30px);
            height: clamp(10px, 1.5vw, 15px);
            border: clamp(2px, 0.4vw, 3px) solid #d81b60;
            border-top: none;
            border-radius: 0 0 30px 30px;
            position: absolute;
            bottom: clamp(10px, 2vw, 15px);
            left: 50%;
            transform: translateX(-50%);
        }

        .cartoon-girl .body {
            width: clamp(35px, 7vw, 60px);
            height: clamp(40px, 8vw, 70px);
            background: linear-gradient(135deg, #ff6b9d 0%, #f06292 100%);
            position: absolute;
            top: clamp(40px, 8vw, 70px);
            left: 50%;
            transform: translateX(-50%);
            border-radius: 30px 30px 15px 15px;
            border: clamp(2px, 0.5vw, 4px) solid #c2185b;
            box-shadow: inset -3px -3px 10px rgba(0,0,0,0.2),
                        0 5px 15px rgba(0,0,0,0.3);
        }

        .cartoon-girl .arm-left,
        .cartoon-girl .arm-right {
            width: clamp(30px, 5vw, 50px);
            height: clamp(10px, 2vw, 18px);
            background: linear-gradient(135deg, #ffcdd2 0%, #ef9a9a 100%);
            position: absolute;
            top: clamp(50px, 9vw, 85px);
            border-radius: 15px;
            border: clamp(2px, 0.4vw, 3px) solid #e91e63;
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-girl .arm-left { 
            left: clamp(-5px, -1vw, -10px); 
            transform: rotate(-30deg);
            transform-origin: right;
        }

        .cartoon-girl .arm-right { 
            right: clamp(-5px, -1vw, -10px); 
            transform: rotate(30deg);
            transform-origin: left;
        }

        .cartoon-girl .leg-left,
        .cartoon-girl .leg-right {
            width: clamp(12px, 2.5vw, 20px);
            height: clamp(35px, 7vw, 60px);
            background: linear-gradient(135deg, #ff6b9d 0%, #f06292 100%);
            position: absolute;
            top: clamp(80px, 15vw, 140px);
            border-radius: 12px;
            border: clamp(2px, 0.4vw, 3px) solid #c2185b;
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-girl .leg-left { left: clamp(15px, 3vw, 25px); }
        .cartoon-girl .leg-right { right: clamp(15px, 3vw, 25px); }

        .cartoon-girl .shoe-left,
        .cartoon-girl .shoe-right {
            width: clamp(15px, 3vw, 25px);
            height: clamp(8px, 1.5vw, 12px);
            background: #000;
            position: absolute;
            bottom: clamp(-8px, -1.5vw, -12px);
            border-radius: 8px 8px 4px 4px;
            left: clamp(-2px, -0.3vw, -2px);
        }

        /* 3D Cartoon Man - Responsive */
        .cartoon-man {
            position: relative;
            width: clamp(80px, 15vw, 140px);
            height: clamp(120px, 22vw, 200px);
            transform-style: preserve-3d;
            filter: drop-shadow(5px 5px 10px rgba(0,0,0,0.4));
        }

        .cartoon-man .head {
            width: clamp(40px, 8vw, 70px);
            height: clamp(40px, 8vw, 70px);
            background: linear-gradient(135deg, #bbdefb 0%, #90caf9 100%);
            border-radius: 50%;
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            border: clamp(3px, 0.5vw, 5px) solid #1976d2;
            box-shadow: inset -3px -3px 10px rgba(0,0,0,0.2),
                        0 5px 15px rgba(0,0,0,0.3);
        }

        .cartoon-man .hair {
            width: clamp(40px, 8vw, 70px);
            height: clamp(20px, 4vw, 35px);
            background: linear-gradient(135deg, #3e2723 0%, #1b0000 100%);
            border-radius: 50% 50% 0 0;
            position: absolute;
            top: clamp(-10px, -2vw, -18px);
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-man .eye-left,
        .cartoon-man .eye-right {
            width: clamp(8px, 1.5vw, 14px);
            height: clamp(8px, 1.5vw, 14px);
            background: #000;
            border-radius: 50%;
            position: absolute;
            top: clamp(15px, 3vw, 25px);
        }

        .cartoon-man .eye-left { left: clamp(10px, 2vw, 18px); }
        .cartoon-man .eye-right { right: clamp(10px, 2vw, 18px); }

        .cartoon-man .eye-left::after,
        .cartoon-man .eye-right::after {
            content: '';
            width: clamp(3px, 0.6vw, 6px);
            height: clamp(3px, 0.6vw, 6px);
            background: white;
            border-radius: 50%;
            position: absolute;
            top: 2px;
            left: 2px;
        }

        .cartoon-man .smile {
            width: clamp(18px, 3vw, 30px);
            height: clamp(10px, 1.5vw, 15px);
            border: clamp(2px, 0.4vw, 3px) solid #0d47a1;
            border-top: none;
            border-radius: 0 0 30px 30px;
            position: absolute;
            bottom: clamp(10px, 2vw, 15px);
            left: 50%;
            transform: translateX(-50%);
        }

        .cartoon-man .body {
            width: clamp(38px, 7.5vw, 65px);
            height: clamp(42px, 8.5vw, 75px);
            background: linear-gradient(135deg, #42a5f5 0%, #2196f3 100%);
            position: absolute;
            top: clamp(40px, 8vw, 70px);
            left: 50%;
            transform: translateX(-50%);
            border-radius: 30px 30px 15px 15px;
            border: clamp(2px, 0.5vw, 4px) solid #1565c0;
            box-shadow: inset -3px -3px 10px rgba(0,0,0,0.2),
                        0 5px 15px rgba(0,0,0,0.3);
        }

        .cartoon-man .arm-left,
        .cartoon-man .arm-right {
            width: clamp(30px, 5vw, 50px);
            height: clamp(10px, 2vw, 18px);
            background: linear-gradient(135deg, #bbdefb 0%, #90caf9 100%);
            position: absolute;
            top: clamp(50px, 9vw, 85px);
            border-radius: 15px;
            border: clamp(2px, 0.4vw, 3px) solid #1976d2;
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-man .arm-left { 
            left: clamp(-5px, -1vw, -10px); 
            transform: rotate(-30deg);
            transform-origin: right;
        }

        .cartoon-man .arm-right { 
            right: clamp(-5px, -1vw, -10px); 
            transform: rotate(30deg);
            transform-origin: left;
        }

        .cartoon-man .leg-left,
        .cartoon-man .leg-right {
            width: clamp(13px, 2.6vw, 22px);
            height: clamp(35px, 7vw, 60px);
            background: linear-gradient(135deg, #1e88e5 0%, #1976d2 100%);
            position: absolute;
            top: clamp(80px, 15vw, 140px);
            border-radius: 12px;
            border: clamp(2px, 0.4vw, 3px) solid #0d47a1;
            box-shadow: 0 3px 8px rgba(0,0,0,0.3);
        }

        .cartoon-man .leg-left { left: clamp(15px, 3vw, 25px); }
        .cartoon-man .leg-right { right: clamp(15px, 3vw, 25px); }

        .cartoon-man .shoe-left,
        .cartoon-man .shoe-right {
            width: clamp(16px, 3.2vw, 28px);
            height: clamp(8px, 1.5vw, 12px);
            background: #000;
            position: absolute;
            bottom: clamp(-8px, -1.5vw, -12px);
            border-radius: 8px 8px 4px 4px;
            left: clamp(-2px, -0.4vw, -3px);
        }

        /* Walking Animation */
        .walking-3d .leg-left {
            animation: leg3DWalkLeft 0.6s ease-in-out infinite;
        }

        .walking-3d .leg-right {
            animation: leg3DWalkRight 0.6s ease-in-out infinite;
        }

        .walking-3d .arm-left {
            animation: arm3DWalkLeft 0.6s ease-in-out infinite;
        }

        .walking-3d .arm-right {
            animation: arm3DWalkRight 0.6s ease-in-out infinite;
        }

        @keyframes leg3DWalkLeft {
            0%, 100% { transform: rotate(-15deg); }
            50% { transform: rotate(25deg); }
        }

        @keyframes leg3DWalkRight {
            0%, 100% { transform: rotate(15deg); }
            50% { transform: rotate(-25deg); }
        }

        @keyframes arm3DWalkLeft {
            0%, 100% { transform: rotate(-30deg); }
            50% { transform: rotate(-60deg); }
        }

        @keyframes arm3DWalkRight {
            0%, 100% { transform: rotate(30deg); }
            50% { transform: rotate(60deg); }
        }

        /* ===== SCENE 1 ===== */
        #scene1 {
            background: linear-gradient(to bottom, #87ceeb 0%, #ffd89b 50%, #90ee90 100%);
        }

        .ground {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 35%;
            background: linear-gradient(to bottom, #8bc34a 0%, #689f38 100%);
            box-shadow: inset 0 8px 20px rgba(0,0,0,0.2);
        }

        .street {
            position: absolute;
            bottom: 30%;
            width: 100%;
            height: clamp(6px, 1vw, 12px);
            background: #555;
            border-top: clamp(2px, 0.5vw, 4px) dashed #fff;
            box-shadow: 0 3px 10px rgba(0,0,0,0.3);
        }

        .sun {
            position: absolute;
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            background: radial-gradient(circle, #ffeb3b 0%, #ffc107 100%);
            border-radius: 50%;
            top: 8%;
            right: 8%;
            box-shadow: 0 0 clamp(30px, 5vw, 60px) #ffd700;
            animation: sunGlow 3s ease-in-out infinite;
        }

        @keyframes sunGlow {
            0%, 100% { box-shadow: 0 0 clamp(30px, 5vw, 60px) #ffd700; }
            50% { box-shadow: 0 0 clamp(50px, 8vw, 100px) #ffd700; }
        }

        #scene1 .cartoon-girl {
            position: absolute;
            left: -20%;
            bottom: 32%;
            animation: girl3DWalk1 7s ease-in-out forwards;
        }

        .wrapper-3d {
            position: absolute;
            width: clamp(25px, 5vw, 40px);
            height: clamp(30px, 6vw, 50px);
            background: linear-gradient(135deg, #fff59d 0%, #ffd54f 100%);
            border-radius: 5px;
            left: 40%;
            bottom: 32%;
            opacity: 0;
            animation: wrapper3DDrop 7s ease-in-out forwards;
            border: 2px solid #f9a825;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .wrapper-shine {
            position: absolute;
            width: 40%;
            height: 50%;
            background: rgba(255,255,255,0.6);
            top: 5px;
            left: 5px;
            border-radius: 3px;
        }

        #scene1 .cartoon-man {
            position: absolute;
            left: -30%;
            bottom: 32%;
            animation: man3DWalk1 9s ease-in-out forwards;
        }

        @keyframes girl3DWalk1 {
            0% { left: -20%; }
            55% { left: 35%; }
            100% { left: 110%; }
        }

        @keyframes wrapper3DDrop {
            0%, 35% { opacity: 0; bottom: 55%; }
            40% { opacity: 1; bottom: 34%; }
            45% { bottom: 32%; }
            100% { opacity: 1; bottom: 32%; }
        }

        @keyframes man3DWalk1 {
            0%, 20% { left: -30%; }
            50% { left: 40%; }
            54% { left: 40%; transform: scale(1); }
            58% { left: 40%; transform: scale(0.9) translateY(10px); }
            62% { left: 40%; transform: scale(1); }
            100% { left: 40%; }
        }

        /* ===== SCENE 2 ===== */
        #scene2 {
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 50%, #d299c2 100%);
        }

        .cloud {
            position: absolute;
            width: clamp(80px, 15vw, 120px);
            height: clamp(30px, 6vw, 50px);
            background: white;
            border-radius: 50px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            animation: cloudFloat 20s linear infinite;
        }

        .cloud::before,
        .cloud::after {
            content: '';
            position: absolute;
            background: white;
            border-radius: 50%;
        }

        .cloud::before {
            width: 40%;
            height: 120%;
            top: -60%;
            left: 20%;
        }

        .cloud::after {
            width: 55%;
            height: 160%;
            top: -80%;
            right: 20%;
        }

        .cloud1 { top: 15%; left: -20%; animation-delay: 0s; }
        .cloud2 { top: 25%; left: -25%; animation-delay: 5s; }

        @keyframes cloudFloat {
            0% { transform: translateX(0); }
            100% { transform: translateX(calc(100vw + 25vw)); }
        }

        .park-tree-3d {
            position: absolute;
            width: clamp(70px, 12vw, 120px);
            height: clamp(100px, 18vw, 180px);
            left: 10%;
            bottom: 30%;
        }

        .tree-trunk {
            width: clamp(30px, 5vw, 50px);
            height: clamp(60px, 10vw, 100px);
            background: linear-gradient(135deg, #8d6e63 0%, #6d4c41 100%);
            border-radius: 10px;
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: inset -3px 0 10px rgba(0,0,0,0.3),
                        0 8px 20px rgba(0,0,0,0.4);
        }

        .tree-leaves-3d {
            width: clamp(100px, 18vw, 200px);
            height: clamp(100px, 18vw, 200px);
            background: radial-gradient(circle, #81c784 0%, #66bb6a 50%, #4caf50 100%);
            border-radius: 50%;
            position: absolute;
            top: -50%;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        #scene2 .cartoon-girl {
            position: absolute;
            left: 20%;
            bottom: 32%;
            animation: girl3DMontage 10s ease-in-out infinite;
        }

        #scene2 .cartoon-man {
            position: absolute;
            left: 0%;
            bottom: 32%;
            animation: man3DMontage 10s ease-in-out infinite;
        }

        @keyframes girl3DMontage {
            0%, 100% { left: 20%; }
            50% { left: 70%; }
        }

        @keyframes man3DMontage {
            0%, 100% { left: 0%; }
            50% { left: 50%; }
        }

        /* ===== SCENE 3: GIFT WRAPPING ===== */
        #scene3 {
            background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 50%, #fbc2eb 100%);
        }

        .room-3d {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 55%;
            background: linear-gradient(to bottom, #d7ccc8 0%, #a1887f 100%);
            box-shadow: inset 0 10px 30px rgba(0,0,0,0.3);
        }

        .desk-3d {
            position: absolute;
            width: clamp(250px, 60vw, 500px);
            height: clamp(130px, 25vw, 250px);
            background: linear-gradient(to bottom, #8d6e63 0%, #6d4c41 100%);
            border-radius: 15px;
            bottom: 28%;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 15px 40px rgba(0,0,0,0.5);
            border: clamp(3px, 0.6vw, 6px) solid #5d4037;
        }

        .chocolate-box {
            position: absolute;
            width: clamp(60px, 12vw, 120px);
            height: clamp(60px, 12vw, 120px);
            background: linear-gradient(135deg, #6d4c41 0%, #5d4037 100%);
            border-radius: 8px;
            left: 30%;
            top: 35%;
            box-shadow: 0 8px 20px rgba(0,0,0,0.4);
            border: 3px solid #4e342e;
            animation: chocolateShow 8s ease-in-out forwards;
            z-index: 5;
        }

        .chocolate-label {
            position: absolute;
            width: 80%;
            height: 40%;
            background: linear-gradient(135deg, #fff59d 0%, #ffd54f 100%);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border-radius: 3px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: clamp(0.6rem, 2vw, 1.2rem);
            font-weight: 900;
            color: #5d4037;
            border: 2px solid #f9a825;
        }

        @keyframes chocolateShow {
            0%, 15% { opacity: 1; transform: scale(1); }
            20%, 100% { opacity: 0; transform: scale(0); }
        }

        .gift-box-3d {
            position: absolute;
            width: clamp(70px, 13vw, 130px);
            height: clamp(70px, 13vw, 130px);
            background: linear-gradient(135deg, #e53935 0%, #c62828 100%);
            border-radius: 8px;
            left: 50%;
            top: 30%;
            transform: translate(-50%, -50%) scale(0);
            animation: gift3DAppear 8s ease-in-out forwards;
            box-shadow: 0 10px 35px rgba(0,0,0,0.5);
            border: clamp(3px, 0.6vw, 5px) solid #b71c1c;
            z-index: 10;
        }

        .gift-shine {
            position: absolute;
            width: 30%;
            height: 45%;
            background: rgba(255,255,255,0.3);
            top: 8px;
            left: 8px;
            border-radius: 5px;
        }

        .gift-ribbon-h {
            position: absolute;
            width: 105%;
            height: clamp(10px, 2vw, 20px);
            background: linear-gradient(to right, #ffd700 0%, #ffeb3b 50%, #ffd700 100%);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            box-shadow: 0 3px 10px rgba(0,0,0,0.4);
            border: 2px solid #f9a825;
        }

        .gift-ribbon-v {
            position: absolute;
            width: clamp(10px, 2vw, 20px);
            height: 105%;
            background: linear-gradient(to bottom, #ffd700 0%, #ffeb3b 50%, #ffd700 100%);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            box-shadow: 0 3px 10px rgba(0,0,0,0.4);
            border: 2px solid #f9a825;
        }

        .gift-bow-3d {
            position: absolute;
            width: clamp(25px, 5vw, 50px);
            height: clamp(25px, 5vw, 50px);
            background: radial-gradient(circle, #ffeb3b 0%, #ffd700 100%);
            border-radius: 50%;
            top: clamp(-12px, -2vw, -20px);
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 5px 15px rgba(0,0,0,0.4);
            border: 3px solid #f9a825;
        }

        .gift-bow-3d::before,
        .gift-bow-3d::after {
            content: '';
            position: absolute;
            width: clamp(20px, 4vw, 35px);
            height: clamp(15px, 3vw, 25px);
            background: linear-gradient(135deg, #ffd700 0%, #ffeb3b 100%);
            border-radius: 50%;
            border: 2px solid #f9a825;
            box-shadow: 0 3px 10px rgba(0,0,0,0.3);
        }

        .gift-bow-3d::before {
            left: clamp(-20px, -4vw, -35px);
            top: clamp(5px, 1vw, 10px);
            transform: rotate(-45deg);
        }

        .gift-bow-3d::after {
            right: clamp(-20px, -4vw, -35px);
            top: clamp(5px, 1vw, 10px);
            transform: rotate(45deg);
        }

        .gift-tag-3d {
            position: absolute;
            background: white;
            padding: clamp(6px, 1.5vw, 12px) clamp(12px, 3vw, 25px);
            border-radius: 5px;
            font-size: clamp(0.8rem, 2.5vw, 1.4rem);
            color: #e53935;
            font-weight: 900;
            bottom: clamp(-25px, -4vw, -45px);
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            border: 2px solid #e53935;
        }

        @keyframes gift3DAppear {
            0%, 20% { 
                transform: translate(-50%, -50%) scale(0) rotateY(0deg); 
                opacity: 0;
            }
            25% {
                opacity: 1;
                transform: translate(-50%, -50%) scale(0.3) rotateY(90deg);
            }
            50% { 
                transform: translate(-50%, -50%) scale(1.2) rotateY(360deg); 
            }
            70%, 100% { 
                transform: translate(-50%, -50%) scale(1) rotateY(360deg); 
            }
        }

        .hand-3d {
            position: absolute;
            width: clamp(30px, 6vw, 50px);
            height: clamp(30px, 6vw, 50px);
            background: radial-gradient(circle, #ffccbc 0%, #ffab91 100%);
            border-radius: 50% 50% 45% 45%;
            border: 3px solid #ff8a65;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            animation: hands3DMove 2.5s ease-in-out infinite;
        }

        .hand-left-3d {
            left: 25%;
            bottom: 40%;
            transform: rotate(-25deg);
        }

        .hand-right-3d {
            right: 25%;
            bottom: 40%;
            transform: rotate(25deg);
            animation-delay: 1.2s;
        }

        .finger {
            position: absolute;
            width: clamp(8px, 1.5vw, 12px);
            height: clamp(12px, 2.5vw, 20px);
            background: linear-gradient(to bottom, #ffccbc 0%, #ffab91 100%);
            border-radius: 6px;
            border: 2px solid #ff8a65;
        }

        .finger1 { top: -8px; left: 5px; }
        .finger2 { top: -10px; left: 50%; transform: translateX(-50%); }
        .finger3 { top: -8px; right: 5px; }

        @keyframes hands3DMove {
            0%, 100% { transform: translateY(0) scale(1); }
            50% { transform: translateY(-15px) scale(1.1); }
        }

        .step-indicator {
            position: absolute;
            top: clamp(12%, 15vh, 20%);
            right: clamp(5%, 8vw, 8%);
            background: rgba(255,255,255,0.95);
            padding: clamp(10px, 2vw, 20px) clamp(15px, 3vw, 30px);
            border-radius: 12px;
            border: 3px solid #e53935;
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
            font-size: clamp(0.8rem, 2.5vw, 1.5rem);
            font-weight: 900;
            color: #e53935;
        }

        .step-indicator::before {
            content: '📦 Step 1';
            animation: stepText 8s steps(1) forwards;
        }

        @keyframes stepText {
            0%, 20% { content: '📦 Step 1'; }
            20%, 50% { content: '🎁 Step 2'; }
            50%, 100% { content: '✨ Ready!'; }
        }

        /* ===== SCENE 4: REJECTION ===== */
        #scene4 {
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 50%, #ff9a9e 100%);
        }

        .fountain-3d {
            position: absolute;
            width: clamp(150px, 30vw, 300px);
            height: clamp(70px, 14vw, 140px);
            background: linear-gradient(to bottom, #4fc3f7 0%, #0288d1 100%);
            border-radius: 50%;
            bottom: 28%;
            left: 60%;
            box-shadow: inset 0 -20px 40px rgba(0,0,0,0.3),
                        0 10px 30px rgba(0,0,0,0.4);
            border: clamp(3px, 0.6vw, 6px) solid #01579b;
        }

        .water-spray {
            position: absolute;
            width: clamp(8px, 1.5vw, 15px);
            height: clamp(8px, 1.5vw, 15px);
            background: radial-gradient(circle, #e3f2fd 0%, #81d4fa 100%);
            border-radius: 50%;
            animation: water3DSpray 1.8s ease-in-out infinite;
            box-shadow: 0 0 10px #81d4fa;
        }

        .spray1 { left: 42%; animation-delay: 0s; }
        .spray2 { left: 50%; animation-delay: 0.6s; }
        .spray3 { left: 58%; animation-delay: 1.2s; }

        @keyframes water3DSpray {
            0% { bottom: 32%; opacity: 1; }
            100% { bottom: 90%; opacity: 0; }
        }

        #scene4 .cartoon-girl {
            position: absolute;
            left: 68%;
            bottom: 30%;
        }

        .girl-speech {
            position: absolute;
            left: 60%;
            top: 30%;
            background: white;
            padding: clamp(8px, 2vw, 15px) clamp(12px, 3vw, 25px);
            border-radius: 15px;
            font-size: clamp(0.9rem, 3vw, 1.6rem);
            font-weight: 900;
            color: #e53935;
            border: 3px solid #c62828;
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
            opacity: 0;
            animation: girlSpeech 10s ease-in-out forwards;
            max-width: 35%;
        }

        .girl-speech::after {
            content: '';
            position: absolute;
            width: 0;
            height: 0;
            border-left: 15px solid transparent;
            border-right: 15px solid transparent;
            border-top: 20px solid white;
            bottom: -20px;
            left: 20px;
        }

        @keyframes girlSpeech {
            0%, 65% { opacity: 0; transform: scale(0); }
            70%, 95% { opacity: 1; transform: scale(1); }
            100% { opacity: 0; transform: scale(0.8); }
        }

        #scene4 .cartoon-man {
            position: absolute;
            left: 3%;
            bottom: 30%;
            animation: man3DApproach 6s ease-in-out forwards;
        }

        @keyframes man3DApproach {
            0% { left: 3%; }
            50%, 100% { left: 42%; }
        }

        .gift-flying-3d {
            position: absolute;
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            background: linear-gradient(135deg, #e53935 0%, #c62828 100%);
            border-radius: 8px;
            left: 47%;
            bottom: 55%;
            opacity: 0;
            animation: gift3DThrow 5s ease-in-out 4s forwards;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            border: 3px solid #b71c1c;
            z-index: 50;
        }

        @keyframes gift3DThrow {
            0% { 
                left: 47%; 
                bottom: 55%; 
                opacity: 1; 
                transform: rotate(0deg) scale(1); 
            }
            30% { 
                left: 42%; 
                bottom: 80%; 
                opacity: 1; 
                transform: rotate(180deg) scale(1.2); 
            }
            60% { 
                left: 35%; 
                bottom: 60%; 
                opacity: 1; 
                transform: rotate(360deg) scale(1); 
            }
            90% { 
                left: 32%; 
                bottom: 48%; 
                opacity: 1; 
                transform: rotate(540deg) scale(0.6); 
            }
            100% { 
                left: 31%; 
                bottom: 43%; 
                opacity: 0; 
                transform: rotate(720deg) scale(0.2); 
            }
        }

        .dustbin-3d {
            position: absolute;
            width: clamp(55px, 11vw, 110px);
            height: clamp(65px, 13vw, 130px);
            background: linear-gradient(to bottom, #616161 0%, #424242 100%);
            border-radius: 8px;
            left: 30%;
            bottom: 28%;
            border: clamp(3px, 0.6vw, 5px) solid #212121;
            box-shadow: 0 10px 35px rgba(0,0,0,0.5);
            z-index: 40;
        }

        .dustbin-lid-3d {
            position: absolute;
            width: 110%;
            height: clamp(10px, 2vw, 18px);
            background: linear-gradient(to bottom, #757575 0%, #616161 100%);
            border-radius: 8px;
            top: -8px;
            left: -5%;
            border: 3px solid #424242;
            box-shadow: 0 6px 15px rgba(0,0,0,0.4);
            animation: lidOpen 5s ease-in-out 8s forwards;
        }

        @keyframes lidOpen {
            0%, 60% { transform: rotateX(0deg); }
            70%, 90% { transform: rotateX(-25deg); transform-origin: top; }
            100% { transform: rotateX(0deg); }
        }

        .trash-icon {
            position: absolute;
            font-size: clamp(1.5rem, 5vw, 3rem);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            opacity: 0.4;
        }

        .bin-label-3d {
            position: absolute;
            bottom: 45%;
            left: 30%;
            font-size: clamp(1rem, 3.5vw, 2rem);
            background: rgba(255,255,255,0.95);
            padding: clamp(6px, 1.5vw, 12px) clamp(12px, 3vw, 30px);
            border-radius: 20px;
            color: #d32f2f;
            font-weight: 900;
            opacity: 0;
            animation: binLabel3D 5s ease-in-out 8s forwards;
            border: 3px solid #d32f2f;
            box-shadow: 0 8px 25px rgba(0,0,0,0.4);
            z-index: 45;
        }

        @keyframes binLabel3D {
            0%, 70% { opacity: 0; transform: scale(0); }
            80%, 95% { opacity: 1; transform: scale(1.1); }
            100% { opacity: 1; transform: scale(1); }
        }

        .rejection-text-3d {
            position: absolute;
            left: 50%;
            top: 15%;
            transform: translateX(-50%);
            font-size: clamp(2rem, 7vw, 4rem);
            color: #d32f2f;
            font-weight: 900;
            opacity: 0;
            animation: rejection3D 5s ease-in-out 8.5s forwards;
            text-shadow: 3px 3px 0px rgba(0,0,0,0.3);
            z-index: 100;
        }

        @keyframes rejection3D {
            0%, 80% { opacity: 0; transform: translateX(-50%) scale(0); }
            90%, 100% { opacity: 1; transform: translateX(-50%) scale(1); }
        }

        .heart-break-particles {
            position: absolute;
            left: 50%;
            top: 30%;
            font-size: clamp(1.5rem, 5vw, 3rem);
            animation: particleFloat 2s ease-out infinite;
        }

        @keyframes particleFloat {
            0% { opacity: 1; transform: translateY(0) scale(1); }
            100% { opacity: 0; transform: translateY(-80px) scale(0.5); }
        }

        /* ===== SCENE 5: CRYING ===== */
        #scene5 {
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 50%, #000000 100%);
        }

        #scene5 .cartoon-man {
            position: absolute;
            left: 50%;
            bottom: 38%;
            transform: translateX(-50%);
        }

        #scene5 .cartoon-man .smile {
            border-radius: 30px 30px 0 0;
            border-bottom: none;
            border-top: 3px solid #0d47a1;
            bottom: clamp(12px, 2.5vw, 18px);
        }

        #scene5 .cartoon-man .eye-left,
        #scene5 .cartoon-man .eye-right {
            width: clamp(10px, 2vw, 18px);
            height: clamp(5px, 1vw, 8px);
            border-radius: 0;
        }

        #scene5 .cartoon-man .arm-left,
        #scene5 .cartoon-man .arm-right {
            animation: arms3DCrying 1.5s ease-in-out infinite;
        }

        @keyframes arms3DCrying {
            0%, 100% { transform: rotate(-120deg); }
            50% { transform: rotate(-115deg); }
        }

        .tear-3d {
            position: absolute;
            width: clamp(10px, 2vw, 18px);
            height: clamp(15px, 3vw, 25px);
            background: linear-gradient(to bottom, #64b5f6 0%, #1976d2 100%);
            border-radius: 50% 50% 50% 0;
            transform: rotate(45deg);
            animation: tear3DFall 1.5s ease-in infinite;
            box-shadow: 0 0 15px #64b5f6;
            border: 2px solid #1565c0;
        }

        .tear-3d::before {
            content: '';
            width: 40%;
            height: 40%;
            background: rgba(255,255,255,0.6);
            border-radius: 50%;
            position: absolute;
            top: 5px;
            left: 5px;
        }

        .tear-left-3d {
            left: clamp(15px, 3vw, 28px);
            top: clamp(20px, 4vw, 35px);
            animation-delay: 0s;
        }

        .tear-right-3d {
            right: clamp(15px, 3vw, 28px);
            top: clamp(20px, 4vw, 35px);
            animation-delay: 0.75s;
        }

        @keyframes tear3DFall {
            0% { transform: rotate(45deg) translateY(0); opacity: 1; }
            100% { transform: rotate(45deg) translateY(80px); opacity: 0; }
        }

        .broken-heart-3d {
            position: absolute;
            top: 18%;
            left: 50%;
            transform: translateX(-50%);
            font-size: clamp(3rem, 12vw, 8rem);
            animation: heart3DBreak 4s ease-in-out infinite;
            filter: drop-shadow(0 0 20px #e91e63);
        }

        @keyframes heart3DBreak {
            0%, 100% { transform: translateX(-50%) scale(1); opacity: 0.9; }
            50% { transform: translateX(-50%) scale(1.2); opacity: 1; }
        }

        /* ===== SCENE 6: THE WELL ===== */
        #scene6 {
            background: linear-gradient(135deg, #000000 0%, #1a237e 50%, #000000 100%);
        }

        .moon {
            position: absolute;
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            background: radial-gradient(circle, #fff9c4 0%, #f9fbe7 100%);
            border-radius: 50%;
            top: 10%;
            right: 15%;
            box-shadow: 0 0 clamp(40px, 8vw, 80px) #fff9c4;
        }

        .well-3d {
            position: absolute;
            width: clamp(160px, 32vw, 320px);
            height: clamp(115px, 23vw, 230px);
            background: linear-gradient(to bottom, #455a64 0%, #263238 100%);
            border-radius: 50% 50% 30px 30px;
            bottom: 20%;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: inset 0 20px 50px rgba(0,0,0,0.8),
                        0 15px 45px rgba(0,0,0,0.6);
            border: clamp(4px, 0.8vw, 8px) solid #1a1a1a;
        }

        .well-water-3d {
            position: absolute;
            width: 80%;
            height: clamp(60px, 12vw, 120px);
            background: radial-gradient(ellipse, #0d1821 0%, #000000 100%);
            border-radius: 50%;
            bottom: 15px;
            left: 50%;
            transform: translateX(-50%);
            box-shadow: 0 0 30px rgba(0,200,255,0.4);
        }

        .well-label-3d {
            position: absolute;
            top: 10%;
            left: 50%;
            transform: translateX(-50%);
            font-size: clamp(1rem, 4vw, 2.5rem);
            background: rgba(255,255,255,0.95);
            padding: clamp(8px, 2vw, 15px) clamp(15px, 4vw, 40px);
            border-radius: 20px;
            color: #c62828;
            font-weight: 900;
            border: 3px solid #c62828;
            box-shadow: 0 8px 30px rgba(0,0,0,0.5);
            max-width: 85%;
            text-align: center;
        }

        #scene6 .cartoon-man {
            position: absolute;
            left: 50%;
            bottom: 70%;
            transform: translateX(-50%);
            animation: jump3DDown 5s ease-in forwards;
        }

        @keyframes jump3DDown {
            0% { 
                bottom: 70%; 
                opacity: 1; 
                transform: translateX(-50%) scale(1) rotateZ(0deg); 
            }
            25% { 
                bottom: 55%; 
                opacity: 1; 
                transform: translateX(-50%) scale(0.95) rotateZ(90deg); 
            }
            50% { 
                bottom: 40%; 
                opacity: 1; 
                transform: translateX(-50%) scale(0.85) rotateZ(180deg); 
            }
            75% { 
                bottom: 28%; 
                opacity: 0.7; 
                transform: translateX(-50%) scale(0.6) rotateZ(270deg); 
            }
            100% { 
                bottom: 22%; 
                opacity: 0; 
                transform: translateX(-50%) scale(0.2) rotateZ(360deg); 
            }
        }

        .splash-3d {
            position: absolute;
            width: clamp(75px, 15vw, 150px);
            height: clamp(75px, 15vw, 150px);
            border: clamp(3px, 0.6vw, 6px) solid #64b5f6;
            border-radius: 50%;
            left: 50%;
            bottom: 26%;
            transform: translate(-50%, -50%);
            opacity: 0;
            animation: splash3D 2.5s ease-out 3.5s forwards;
            box-shadow: 0 0 30px #64b5f6;
        }

        @keyframes splash3D {
            0% { transform: translate(-50%, -50%) scale(0.3); opacity: 1; }
            100% { transform: translate(-50%, -50%) scale(2.5); opacity: 0; }
        }

        /* ===== SCENE 7: EPILOGUE ===== */
        #scene7 {
            background: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
            flex-direction: column;
        }

        .stars {
            position: absolute;
            width: clamp(2px, 0.5vw, 3px);
            height: clamp(2px, 0.5vw, 3px);
            background: white;
            border-radius: 50%;
            box-shadow: 0 0 8px white;
            animation: starTwinkle 3s ease-in-out infinite;
        }

        .star1 { top: 15%; left: 20%; animation-delay: 0s; }
        .star2 { top: 25%; left: 80%; animation-delay: 1s; }
        .star3 { top: 40%; left: 10%; animation-delay: 2s; }
        .star4 { top: 60%; right: 15%; animation-delay: 1.5s; }

        @keyframes starTwinkle {
            0%, 100% { opacity: 0.3; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.5); }
        }

        .epilogue-text-3d {
            font-size: clamp(1.2rem, 5vw, 3.2rem);
            text-align: center;
            padding: clamp(1.5rem, 4vw, 3rem);
            line-height: 1.8;
            opacity: 0;
            animation: text3DFadeIn 5s ease-in forwards;
            font-style: italic;
            text-shadow: 2px 2px 15px rgba(0,0,0,0.8);
            max-width: 90%;
            background: rgba(0,0,0,0.6);
            border-radius: 20px;
            backdrop-filter: blur(10px);
            border: 3px solid rgba(255,255,255,0.2);
        }

        @keyframes text3DFadeIn {
            0% { opacity: 0; transform: translateY(30px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        .floating-chocolate-3d {
            position: absolute;
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            background: linear-gradient(135deg, #e53935 0%, #c62828 100%);
            border-radius: 10px;
            bottom: 68%;
            left: 50%;
            transform: translateX(-50%);
            animation: float3DChocolate 5s ease-in-out infinite;
            box-shadow: 0 8px 30px rgba(229,57,53,0.6);
            border: clamp(3px, 0.6vw, 5px) solid #b71c1c;
        }

        .floating-chocolate-3d::before {
            content: '🍫';
            position: absolute;
            font-size: clamp(1.5rem, 5vw, 3rem);
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        @keyframes float3DChocolate {
            0%, 100% { transform: translateX(-50%) translateY(0); }
            50% { transform: translateX(-50%) translateY(-25px); }
        }

        .ripple-3d {
            position: absolute;
            border: clamp(2px, 0.5vw, 4px) solid rgba(255,255,255,0.5);
            border-radius: 50%;
            bottom: 63%;
            left: 50%;
            transform: translate(-50%, -50%);
            animation: ripple3DEffect 4s ease-out infinite;
            box-shadow: 0 0 15px rgba(255,255,255,0.3);
        }

        .ripple1-3d {
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            animation-delay: 0s;
        }

        .ripple2-3d {
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            animation-delay: 1.3s;
        }

        .ripple3-3d {
            width: clamp(50px, 10vw, 100px);
            height: clamp(50px, 10vw, 100px);
            animation-delay: 2.6s;
        }

        @keyframes ripple3DEffect {
            0% { width: clamp(50px, 10vw, 100px); height: clamp(50px, 10vw, 100px); opacity: 1; }
            100% { width: clamp(150px, 30vw, 350px); height: clamp(150px, 30vw, 350px); opacity: 0; }
        }

        /* ===== MOBILE-OPTIMIZED CONTROLS ===== */
        .controls {
            position: fixed;
            bottom: clamp(10px, 2vh, 25px);
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000;
            display: flex;
            gap: clamp(8px, 2vw, 20px);
            background: rgba(0,0,0,0.8);
            padding: clamp(12px, 2.5vh, 20px) clamp(15px, 4vw, 35px);
            border-radius: 50px;
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            box-shadow: 0 10px 35px rgba(0,0,0,0.6);
        }

        .control-btn {
            padding: clamp(10px, 2vh, 15px) clamp(15px, 4vw, 30px);
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border: 2px solid rgba(255,255,255,0.5);
            color: white;
            cursor: pointer;
            border-radius: 25px;
            font-size: clamp(0.9rem, 3vw, 1.2rem);
            font-weight: 900;
            transition: all 0.3s;
            box-shadow: 0 6px 15px rgba(0,0,0,0.3);
            touch-action: manipulation;
            -webkit-tap-highlight-color: transparent;
        }

        .control-btn:active {
            transform: scale(0.95);
        }

        .progress-bar {
            position: fixed;
            top: 0;
            left: 0;
            height: clamp(4px, 1vh, 8px);
            background: linear-gradient(90deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
            width: 0%;
            transition: width 0.5s;
            z-index: 1001;
            box-shadow: 0 2px 10px rgba(102,126,234,0.6);
        }

        .music-indicator {
            position: fixed;
            top: clamp(12px, 2vh, 25px);
            right: clamp(12px, 2vw, 25px);
            z-index: 1000;
            display: flex;
            align-items: center;
            gap: clamp(8px, 2vw, 15px);
            background: rgba(0,0,0,0.8);
            padding: clamp(10px, 2vh, 15px) clamp(15px, 3vw, 30px);
            border-radius: 30px;
            backdrop-filter: blur(10px);
            cursor: pointer;
            border: 2px solid rgba(255,255,255,0.3);
            box-shadow: 0 8px 25px rgba(0,0,0,0.5);
            touch-action: manipulation;
        }

        .music-bars {
            display: flex;
            gap: clamp(3px, 0.6vw, 5px);
            align-items: flex-end;
            height: clamp(16px, 3vh, 28px);
        }

        .music-bar {
            width: clamp(3px, 0.6vw, 5px);
            background: linear-gradient(to top, #667eea 0%, #f093fb 100%);
            border-radius: 4px;
            animation: music3DPulse 0.9s ease-in-out infinite;
        }

        .bar1 { height: 50%; animation-delay: 0s; }
        .bar2 { height: 75%; animation-delay: 0.2s; }
        .bar3 { height: 100%; animation-delay: 0.4s; }
        .bar4 { height: 70%; animation-delay: 0.6s; }

        @keyframes music3DPulse {
            0%, 100% { transform: scaleY(0.5); opacity: 0.7; }
            50% { transform: scaleY(1); opacity: 1; }
        }

        .music-indicator.muted .music-bar {
            animation: none;
            opacity: 0.3;
        }

        .scene-counter {
            position: fixed;
            top: clamp(12px, 2vh, 25px);
            left: clamp(12px, 2vw, 25px);
            z-index: 1000;
            background: rgba(0,0,0,0.8);
            padding: clamp(10px, 2vh, 15px) clamp(15px, 3vw, 30px);
            border-radius: 30px;
            backdrop-filter: blur(10px);
            font-size: clamp(0.8rem, 2.5vw, 1.3rem);
            font-weight: 900;
            border: 2px solid rgba(255,255,255,0.3);
            box-shadow: 0 8px 25px rgba(0,0,0,0.5);
            max-width: 40%;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        /* Mobile-specific optimizations */
        @media (max-width: 768px) {
            .scene-counter {
                font-size: 0.75rem;
            }

            .scene-title {
                font-size: 1rem;
                padding: 8px 15px;
            }

            .scene-description {
                font-size: 0.7rem;
                padding: 8px 12px;
            }

            .girl-speech {
                max-width: 50%;
                left: 55%;
            }
        }

        @media (max-width: 480px) {
            .controls {
                gap: 6px;
                padding: 10px 12px;
            }

            .control-btn {
                padding: 8px 12px;
                font-size: 0.8rem;
            }
        }

        /* Landscape mobile */
        @media (max-height: 500px) and (orientation: landscape) {
            .scene-title {
                top: 2%;
                font-size: 1rem;
                padding: 5px 15px;
            }

            .scene-description {
                bottom: 5%;
                font-size: 0.7rem;
                padding: 5px 12px;
            }

            .controls {
                bottom: 8px;
                padding: 8px 12px;
            }

            .cartoon-girl,
            .cartoon-man {
                transform: scale(0.8);
            }
        }
    </style>
</head>
<body>
    <div class="progress-bar" id="progressBar"></div>
    
    <div class="scene-counter" id="sceneCounter">🎬 Start</div>
    
    <div class="music-indicator" id="musicToggle">
        <div class="music-bars">
            <div class="music-bar bar1"></div>
            <div class="music-bar bar2"></div>
            <div class="music-bar bar3"></div>
            <div class="music-bar bar4"></div>
        </div>
        <span style="font-size: clamp(1rem, 3vw, 1.5rem);">♪</span>
    </div>

    <div id="animation-container">
        <!-- Start Screen -->
        <div class="scene active" id="start-screen">
            <h1>💔 Unseen Love 💔</h1>
            <p>A 3D Cartoon Love Story</p>
            <p style="font-size: clamp(0.8rem, 2.5vw, 1.2rem); opacity: 0.8; margin-top: 10px;">⏱️ Duration: ~2 minutes</p>
            <button id="start-btn">▶ Begin the Journey</button>
        </div>

        <!-- Scene 1: Morning Street -->
        <div class="scene" id="scene1">
            <div class="scene-title">🌅 Scene 1: First Encounter</div>
            <div class="scene-description">A beautiful morning... A girl walks, unknowingly dropping something...</div>
            
            <div class="sun"></div>
            <div class="ground"></div>
            <div class="street"></div>
            
            <div class="cartoon-girl walking-3d">
                <div class="head">
                    <div class="hair">
                        <div class="ponytail"></div>
                    </div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
            
            <div class="wrapper-3d">
                <div class="wrapper-shine"></div>
            </div>
            
            <div class="cartoon-man walking-3d">
                <div class="head">
                    <div class="hair"></div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
        </div>

        <!-- Scene 2: Montage -->
        <div class="scene" id="scene2">
            <div class="scene-title">📅 Scene 2: Days of Silent Love</div>
            <div class="scene-description">Every day, he follows her... cleaning up after her... loving silently...</div>
            
            <div class="cloud cloud1"></div>
            <div class="cloud cloud2"></div>
            <div class="ground"></div>
            <div class="park-tree-3d">
                <div class="tree-leaves-3d"></div>
                <div class="tree-trunk"></div>
            </div>
            
            <div class="cartoon-girl walking-3d">
                <div class="head">
                    <div class="hair">
                        <div class="ponytail"></div>
                    </div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
            
            <div class="cartoon-man walking-3d">
                <div class="head">
                    <div class="hair"></div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
        </div>

        <!-- Scene 3: The Gift - SUPER CLEAR -->
        <div class="scene" id="scene3">
            <div class="scene-title">🎁 Scene 3: Preparing the Perfect Gift</div>
            <div class="scene-description">With love and care, he wraps a chocolate box for her birthday...</div>
            
            <div class="room-3d"></div>
            <div class="desk-3d">
                <div class="chocolate-box">
                    <div class="chocolate-label">🍫 CHOCOLATE</div>
                </div>
                
                <div class="gift-box-3d">
                    <div class="gift-shine"></div>
                    <div class="gift-ribbon-h"></div>
                    <div class="gift-ribbon-v"></div>
                    <div class="gift-bow-3d"></div>
                    <div class="gift-tag-3d">🎂 Happy Birthday!</div>
                </div>
            </div>
            
            <div class="hand-3d hand-left-3d">
                <div class="finger finger1"></div>
                <div class="finger finger2"></div>
                <div class="finger finger3"></div>
            </div>
            <div class="hand-3d hand-right-3d">
                <div class="finger finger1"></div>
                <div class="finger finger2"></div>
                <div class="finger finger3"></div>
            </div>
            
            <div class="step-indicator"></div>
        </div>

        <!-- Scene 4: The Birthday - SUPER CLEAR REJECTION -->
        <div class="scene" id="scene4">
            <div class="scene-title">💔 Scene 4: November 19 - Her Birthday</div>
            <div class="scene-description">He approaches with hope and love... but then...</div>
            
            <div class="ground"></div>
            <div class="fountain-3d">
                <div class="water-spray spray1"></div>
                <div class="water-spray spray2"></div>
                <div class="water-spray spray3"></div>
            </div>
            
            <div class="dustbin-3d">
                <div class="dustbin-lid-3d"></div>
                <div class="trash-icon">🗑️</div>
            </div>
            <div class="bin-label-3d">⚠️ TRASH!</div>
            
            <div class="cartoon-girl">
                <div class="head">
                    <div class="hair">
                        <div class="ponytail"></div>
                    </div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
            
            <div class="girl-speech">I don't want this! 😒</div>
            
            <div class="cartoon-man walking-3d">
                <div class="head">
                    <div class="hair"></div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
            
            <div class="gift-flying-3d">
                <div class="gift-ribbon-h"></div>
                <div class="gift-ribbon-v"></div>
            </div>
            
            <div class="rejection-text-3d">REJECTED! 💔</div>
            <div class="heart-break-particles particle1" style="left: 50%; animation-delay: 0s;">💔</div>
            <div class="heart-break-particles particle2" style="left: 55%; animation-delay: 0.5s;">💔</div>
            <div class="heart-break-particles particle3" style="left: 45%; animation-delay: 1s;">💔</div>
        </div>

        <!-- Scene 5: The Breakdown -->
        <div class="scene" id="scene5">
            <div class="scene-title">😢 Scene 5: Heartbreak</div>
            <div class="scene-description">His heart shatters... tears fall... pain overwhelms...</div>
            
            <div class="broken-heart-3d">💔</div>
            
            <div class="cartoon-man">
                <div class="head">
                    <div class="hair"></div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
                <div class="tear-3d tear-left-3d"></div>
                <div class="tear-3d tear-right-3d"></div>
            </div>
        </div>

        <!-- Scene 6: The Well -->
        <div class="scene" id="scene6">
            <div class="scene-title">🌑 Scene 6: The Well</div>
            <div class="scene-description">In despair, he makes a final choice...</div>
            
            <div class="moon"></div>
            <div class="well-label-3d">⚠️ OLD WELL - DANGER!</div>
            <div class="well-3d">
                <div class="well-water-3d"></div>
            </div>
            
            <div class="cartoon-man">
                <div class="head">
                    <div class="hair"></div>
                    <div class="eye-left"></div>
                    <div class="eye-right"></div>
                    <div class="smile"></div>
                </div>
                <div class="body"></div>
                <div class="arm-left"></div>
                <div class="arm-right"></div>
                <div class="leg-left">
                    <div class="shoe-left"></div>
                </div>
                <div class="leg-right">
                    <div class="shoe-right"></div>
                </div>
            </div>
            
            <div class="splash-3d"></div>
        </div>

        <!-- Scene 7: Epilogue -->
        <div class="scene" id="scene7">
            <div class="scene-title" style="background: rgba(255,255,255,0.1);">✨ Epilogue</div>
            
            <div class="stars star1"></div>
            <div class="stars star2"></div>
            <div class="stars star3"></div>
            <div class="stars star4"></div>
            
            <div class="floating-chocolate-3d"></div>
            <div class="ripple-3d ripple1-3d"></div>
            <div class="ripple-3d ripple2-3d"></div>
            <div class="ripple-3d ripple3-3d"></div>
            <div class="epilogue-text-3d">
                💔<br><br>
                "Some love is silent.<br>
                Some pain is unseen.<br>
                Some hearts break in silence."<br><br>
                <span style="font-size: clamp(1rem, 3vw, 2rem);">- The End -</span>
            </div>
        </div>
    </div>

    <div class="controls">
        <button class="control-btn" id="restartBtn">↺</button>
        <button class="control-btn" id="pauseBtn">⏸</button>
        <button class="control-btn" id="nextBtn">→</button>
    </div>

    <script>
        const scenes = [
            { id: 'start-screen', duration: 0, name: '🎬 Start' },
            { id: 'scene1', duration: 9000, name: '🌅 First Encounter' },
            { id: 'scene2', duration: 11000, name: '📅 Silent Love' },
            { id: 'scene3', duration: 10000, name: '🎁 The Gift' },
            { id: 'scene4', duration: 12000, name: '💔 Rejection' },
            { id: 'scene5', duration: 7000, name: '😢 Heartbreak' },
            { id: 'scene6', duration: 8000, name: '🌑 The Well' },
            { id: 'scene7', duration: 13000, name: '✨ Epilogue' }
        ];

        let currentSceneIndex = 0;
        let isPaused = false;
        let sceneTimeout;
        let audioContext;
        let isMuted = false;

        function initAudio() {
            audioContext = new (window.AudioContext || window.webkitAudioContext)();
        }

        function playNote(frequency, duration, delay = 0, volume = 0.12) {
            if (isMuted || !audioContext) return;
            setTimeout(() => {
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                oscillator.frequency.value = frequency;
                oscillator.type = 'sine';
                gainNode.gain.setValueAtTime(volume, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + duration);
            }, delay);
        }

        const melodyPattern = [
            { note: 329.63, duration: 1.5 },
            { note: 293.66, duration: 1.5 },
            { note: 261.63, duration: 1.5 },
            { note: 246.94, duration: 2 },
            { note: 293.66, duration: 1.5 },
            { note: 261.63, duration: 1.5 },
            { note: 246.94, duration: 2 },
            { note: 220.00, duration: 3 }
        ];

        let melodyInterval;

        function startMelody() {
            if (isMuted) return;
            let time = 0;
            melodyPattern.forEach(({ note, duration }) => {
                playNote(note, duration, time * 1000, 0.1);
                time += duration;
            });
            melodyInterval = setInterval(() => {
                let time = 0;
                melodyPattern.forEach(({ note, duration }) => {
                    playNote(note, duration, time * 1000, 0.1);
                    time += duration;
                });
            }, 13000);
        }

        function stopMelody() {
            if (melodyInterval) clearInterval(melodyInterval);
        }

        function showScene(index) {
            document.querySelectorAll('.scene').forEach(scene => scene.classList.remove('active'));
            if (index < scenes.length) {
                document.getElementById(scenes[index].id).classList.add('active');
                currentSceneIndex = index;
                document.getElementById('sceneCounter').textContent = scenes[index].name;
                document.getElementById('progressBar').style.width = (index / (scenes.length - 1)) * 100 + '%';
                if (scenes[index].duration > 0 && !isPaused) {
                    sceneTimeout = setTimeout(() => {
                        if (currentSceneIndex < scenes.length - 1) {
                            showScene(currentSceneIndex + 1);
                        } else {
                            setTimeout(() => showScene(0), 3000);
                        }
                    }, scenes[index].duration);
                }
            }
        }

        document.getElementById('start-btn').addEventListener('click', () => {
            initAudio();
            startMelody();
            showScene(1);
        });

        document.getElementById('restartBtn').addEventListener('click', () => {
            clearTimeout(sceneTimeout);
            isPaused = false;
            stopMelody();
            initAudio();
            startMelody();
            showScene(1);
            document.getElementById('pauseBtn').textContent = '⏸';
        });

        document.getElementById('pauseBtn').addEventListener('click', () => {
            isPaused = !isPaused;
            if (isPaused) {
                clearTimeout(sceneTimeout);
                document.getElementById('pauseBtn').textContent = '▶';
            } else {
                document.getElementById('pauseBtn').textContent = '⏸';
                showScene(currentSceneIndex);
            }
        });

        document.getElementById('nextBtn').addEventListener('click', () => {
            clearTimeout(sceneTimeout);
            if (currentSceneIndex === 0) {
                initAudio();
                startMelody();
                showScene(1);
            } else if (currentSceneIndex < scenes.length - 1) {
                showScene(currentSceneIndex + 1);
            } else {
                showScene(0);
            }
        });

        document.getElementById('musicToggle').addEventListener('click', () => {
            isMuted = !isMuted;
            const musicIndicator = document.getElementById('musicToggle');
            if (isMuted) {
                musicIndicator.classList.add('muted');
                stopMelody();
            } else {
                musicIndicator.classList.remove('muted');
                if (currentSceneIndex > 0) startMelody();
            }
        });

        // Touch-friendly controls
        document.querySelectorAll('.control-btn, .music-indicator, #start-btn').forEach(btn => {
            btn.addEventListener('touchstart', function(e) {
                this.style.transform = 'scale(0.95)';
            });
            btn.addEventListener('touchend', function(e) {
                this.style.transform = 'scale(1)';
            });
        });

        // Prevent double-tap zoom
        let lastTouchEnd = 0;
        document.addEventListener('touchend', function(e) {
            const now = Date.now();
            if (now - lastTouchEnd <= 300) {
                e.preventDefault();
            }
            lastTouchEnd = now;
        }, false);

        console.log('%c🎬 Unseen Love - Mobile Responsive Edition', 'font-size: 16px; font-weight: bold; color: #e91e63;');
        console.log('%c📱 Optimized for all screen sizes!', 'font-size: 12px; color: #2196f3;');
    </script>
</body>
</html>