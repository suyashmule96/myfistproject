<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    import React, { useState, useEffect, useRef } from 'react';
// Removed: import L from 'leaflet'; // Leaflet will be loaded via CDN
// Removed: import 'leaflet/dist/leaflet.css'; // Leaflet CSS will be loaded via CDN

// --- Translations ---
const translations = {
  en: {
    home: "Home",
    schemes: "Schemes",
    products: "Products",
    learning: "Learning",
    awards: "Awards",
    demand: "Market Demand",
    certification: "Certifications",
    scanner: "AI Scanner",
    weather: "Weather",
    login: "Login",
    register: "Register",
    logout: "Logout",
    welcome: "Welcome to Organic Farm Hub!",
    tagline: "Your one-stop solution for sustainable agriculture.",
    aboutUs: "About Us",
    aboutUsContent: "Organic Farm Hub is dedicated to promoting organic farming practices, connecting farmers with resources, and providing consumers with access to healthy, organic produce. Our mission is to foster a sustainable agricultural ecosystem for a healthier planet and prosperous farming communities.",
    govSchemes: "Government Schemes",
    generalFarmerSchemes: "General Farmer Welfare Schemes",
    autonomousBodies: "Autonomous Government Organizations & Support Bodies",
    privateSchemes: "Private Initiatives",
    schemeTitle: "Scheme Name",
    schemeDesc: "Description",
    schemeEligibility: "Eligibility",
    schemeBenefits: "Benefits",
    schemeLink: "More Info",
    productCatalog: "Organic Products Catalog",
    searchProduct: "Search Product...",
    comparePrices: "Compare Prices",
    bestPrice: "Best Price!",
    loadingPrices: "Loading prices...",
    priceError: "Could not fetch prices. Please try again later.",
    learningResources: "Learning & Study Materials",
    studyMaterials: "Study Materials",
    youtubeVideos: "YouTube Videos",
    beginnerGuides: "Beginner Guides",
    advancedTopics: "Advanced Topics",
    universityCourses: "University Courses",
    govPublications: "Government Publications",
    awardsRecognition: "Awards & Recognition",
    nationalAwards: "National Awards",
    internationalAwards: "International Awards",
    awardName: "Award Name",
    awardOrg: "Organizing Body",
    awardYear: "Year",
    awardWinners: "Winners/Recipients",
    marketDemand: "Market Demand & Trends",
    demandOverview: "Overall Market Demand",
    componentDemand: "Component Demand",
    demandMap: "Demand Distribution Map (India)",
    mapDisclaimer: "Demand data is indicative and based on available market research. For precise figures, consult official reports.",
    aiScanner: "AI Powered Scanner",
    uploadImage: "Upload Image",
    scan: "Scan for Diagnosis",
    scannerPlaceholder: "Upload an image of your plant or pest for an AI-powered diagnosis and organic solutions.",
    scanning: "Scanning...",
    scannerResult: "AI Diagnosis Result",
    noImage: "Please upload an image to scan.",
    certificationInfo: "Organic Certification & Exams",
    certGov: "Government Certifications",
    certPrivate: "Private Certifications",
    certExamModule: "Certification Exam Module (Practice)",
    uploadCertificates: "Upload Your Certificates (7/12, 8A)",
    email: "Email",
    password: "Password",
    farmerId: "Government Farmer ID",
    upload: "Upload",
    fileUploadDisclaimer: "Please upload digitally signed copies. This is for your record-keeping on our platform only. Official verification requires government portals.",
    fileUploaded: "File uploaded successfully!",
    loginSuccess: "Login Successful!",
    loginFailed: "Invalid Email or Password.",
    registerSuccess: "Registration Successful! Please login.",
    registerFailed: "Registration failed. Please try again.",
    emailRequired: "Email is required.",
    passwordRequired: "Password is required.",
    invalidEmail: "Invalid email format.",
    passwordMinLength: "Password must be at least 6 characters.",
    farmerIdOptional: "Farmer ID (optional for linking, NOT as password)",
    confirmPassword: "Confirm Password",
    passwordsMismatch: "Passwords do not match.",
    requiredField: "This field is required.",
    viewProfile: "View Profile",
    upload712: "Upload 7/12 Extract",
    upload8A: "Upload 8A Extract",
    userDocuments: "Your Uploaded Documents",
    noDocuments: "No documents uploaded yet.",
    documentType: "Document Type",
    fileName: "File Name",
    uploadedOn: "Uploaded On",
    status: "Status",
    pending: "Pending Verification",
    verified: "Verified",
    download: "Download",
    contactUs: "Contact Us",
    contactInfo: "For any queries, please reach out to us:",
    emailAddress: "suyashmule16@gmail.com",
    phoneNumber: "+91 8468846995",
    yourName: "Your Name",
    subject: "Subject",
    message: "Message",
    sendMessage: "Send Message",
    messageSentSuccess: "Thank you for your message! We will get back to you soon.",
    messageSentError: "Failed to send message. Please try again later.",
    followUs: "Follow Us",
    footerText: "© 2025 Organic Farm Hub. All rights reserved.",
    visitYouTube: "Visit YouTube for More",
    onlineCourses: "Online Certification Courses & Resources",
    updatePrices: "Update Prices",
    officialSites: "Official Retail Sites",
    weatherAdvisory: "Weather & Advisory",
    currentWeather: "Current Weather",
    forecast: "5-Day Forecast",
    agriAdvisory: "Agricultural Advisory",
    humidity: "Humidity",
    wind: "Wind",
    advisoryHot: "Hot and sunny conditions are expected. Ensure adequate irrigation for standing crops, especially during peak afternoon hours. Check for signs of heat stress in livestock.",
    advisoryRain: "Rain is expected. Ensure proper drainage in fields to prevent waterlogging. Postpone application of fertilizers or pesticides until after the rain.",
    advisoryMixed: "Weather is expected to be variable with cloudy intervals. Monitor crops for pests and diseases that thrive in humid conditions. This is a good time for intercultural operations like weeding.",
    marketPrices: "Market Prices",
    selectState: "Select State",
    selectDistrict: "Select District",
    searchForProduct: "Search for a product...",
    product: "Product",
    category: "Category",
    price: "Price (per Quintal)",
    noPrices: "Please select a state and district to view prices.",
    loading: "Loading Prices...",
  },
  hi: {
    home: "होम",
    schemes: "योजनाएं",
    products: "उत्पाद",
    learning: "सीखें",
    awards: "पुरस्कार",
    demand: "बाजार मांग",
    certification: "प्रमाणीकरण",
    scanner: "एआई स्कैनर",
    weather: "मौसम",
    login: "लॉगिन",
    register: "रजिस्टर करें",
    logout: "लॉगआउट",
    welcome: "ऑर्गेनिक फार्म हब में आपका स्वागत है!",
    tagline: "स्थायी कृषि के लिए आपका वन-स्टॉप समाधान।",
    aboutUs: "हमारे बारे में",
    aboutUsContent: "ऑर्गेनिक फार्म हब जैविक खेती को बढ़ावा देने, किसानों को संसाधनों से जोड़ने और उपभोक्ताओं को स्वस्थ, जैविक उत्पादों तक पहुंच प्रदान करने के लिए समर्पित है। हमारा मिशन एक स्वस्थ ग्रह और समृद्ध कृषि समुदायों के लिए एक स्थायी कृषि पारिस्थितिकी तंत्र को बढ़ावा देना है।",
    govSchemes: "सरकारी योजनाएं",
    generalFarmerSchemes: "सामान्य किसान कल्याण योजनाएं",
    autonomousBodies: "स्वायत्त सरकारी संगठन और सहायता निकाय",
    privateSchemes: "निजी पहल",
    schemeTitle: "योजना का नाम",
    schemeDesc: "विवरण",
    schemeEligibility: "पात्रता",
    schemeBenefits: "लाभ",
    schemeLink: "और जानकारी",
    productCatalog: "जैविक उत्पाद कैटलॉग",
    searchProduct: "उत्पाद खोजें...",
    comparePrices: "कीमतों की तुलना करें",
    bestPrice: "सर्वोत्तम मूल्य!",
    loadingPrices: "कीमतें लोड हो रही हैं...",
    priceError: "कीमतें प्राप्त नहीं हो सकीं। कृपया बाद में पुनः प्रयास करें।",
    learningResources: "सीखने और अध्ययन सामग्री",
    studyMaterials: "अध्ययन सामग्री",
    youtubeVideos: "यूट्यूब वीडियो",
    beginnerGuides: "शुरुआती गाइड",
    advancedTopics: "उन्नत विषय",
    universityCourses: "विश्वविद्यालय पाठ्यक्रम",
    govPublications: "सरकारी प्रकाशन",
    awardsRecognition: "पुरस्कार और मान्यता",
    nationalAwards: "राष्ट्रीय पुरस्कार",
    internationalAwards: "अंतर्राष्ट्रीय पुरस्कार",
    awardName: "पुरस्कार का नाम",
    awardOrg: "आयोजक निकाय",
    awardYear: "वर्ष",
    awardWinners: "विजेता/प्राप्तकर्ता",
    marketDemand: "बाजार मांग और रुझान",
    demandOverview: "कुल बाजार मांग",
    componentDemand: "घटक मांग",
    demandMap: "मांग वितरण मानचित्र (भारत)",
    mapDisclaimer: "मांग डेटा सांकेतिक है और उपलब्ध बाजार अनुसंधान पर आधारित है। सटीक आंकड़ों के लिए, आधिकारिक रिपोर्ट देखें।",
    aiScanner: "एआई संचालित स्कैनर",
    uploadImage: "छवि अपलोड करें",
    scan: "निदान के लिए स्कैन करें",
    scannerPlaceholder: "एआई-संचालित निदान और जैविक समाधानों के लिए अपने पौधे या कीट की एक छवि अपलोड करें।",
    scanning: "स्कैनिंग...",
    scannerResult: "एआई निदान परिणाम",
    noImage: "स्कैन करने के लिए कृपया एक छवि अपलोड करें।",
    certificationInfo: "जैविक प्रमाणीकरण और परीक्षा",
    certGov: "सरकारी प्रमाणीकरण",
    certPrivate: "निजी प्रमाणीकरण",
    certExamModule: "प्रमाणीकरण परीक्षा मॉड्यूल (अभ्यास)",
    uploadCertificates: "अपने प्रमाणपत्र अपलोड करें (7/12, 8A)",
    email: "ईमेल",
    password: "पासवर्ड",
    farmerId: "सरकारी किसान आईडी",
    upload: "अपलोड करें",
    fileUploadDisclaimer: "कृपया डिजिटल रूप से हस्ताक्षरित प्रतियां अपलोड करें। यह केवल हमारे प्लेटफॉर्म पर आपके रिकॉर्ड रखने के लिए है। आधिकारिक सत्यापन के लिए सरकारी पोर्टल की आवश्यकता होती है।",
    fileUploaded: "फाइल सफलतापूर्वक अपलोड हो गई!",
    loginSuccess: "लॉगिन सफल!",
    loginFailed: "अमान्य ईमेल या पासवर्ड।",
    registerSuccess: "पंजीकरण सफल! कृपया लॉगिन करें।",
    registerFailed: "पंजीकरण विफल रहा। कृपया पुनः प्रयास करें।",
    emailRequired: "ईमेल आवश्यक है।",
    passwordRequired: "पासवर्ड आवश्यक है।",
    invalidEmail: "अमान्य ईमेल प्रारूप।",
    passwordMinLength: "पासवर्ड कम से कम 6 वर्णों का होना चाहिए।",
    farmerIdOptional: "किसान आईडी (लिंक करने के लिए वैकल्पिक, पासवर्ड के रूप में नहीं)",
    confirmPassword: "पासवर्ड की पुष्टि करें",
    passwordsMismatch: "पासवर्ड मेल नहीं खाते।",
    requiredField: "यह फ़ील्ड आवश्यक है।",
    viewProfile: "प्रोफ़ाइल देखें",
    upload712: "7/12 अर्क अपलोड करें",
    upload8A: "8A अर्क अपलोड करें",
    userDocuments: "आपके अपलोड किए गए दस्तावेज़",
    noDocuments: "अभी तक कोई दस्तावेज़ अपलोड नहीं किया गया है।",
    documentType: "दस्तावेज़ का प्रकार",
    fileName: "फ़ाइल का नाम",
    uploadedOn: "अपलोड किया गया",
    status: "स्थिति",
    pending: "सत्यापन लंबित",
    verified: "सत्यापित",
    download: "डाउनलोड करें",
    contactUs: "हमसे संपर्क करें",
    contactInfo: "किसी भी प्रश्न के लिए, कृपया हमसे संपर्क करें:",
    emailAddress: "suyashmule16@gmail.com",
    phoneNumber: "+91 8468846995",
    yourName: "आपका नाम",
    subject: "विषय",
    message: "संदेश",
    sendMessage: "संदेश भेजें",
    messageSentSuccess: "आपके संदेश के लिए धन्यवाद! हम जल्द ही आपसे संपर्क करेंगे।",
    messageSentError: "संदेश भेजने में विफल। कृपया बाद में पुनः प्रयास करें।",
    followUs: "हमें फॉलो करें",
    footerText: "© 2025 ऑर्गेनिक फार्म हब। सर्वाधिकार सुरक्षित।",
    visitYouTube: "और वीडियो के लिए यूट्यूब पर जाएं",
    onlineCourses: "ऑनलाइन प्रमाणन पाठ्यक्रम और संसाधन",
    updatePrices: "कीमतें अपडेट करें",
    officialSites: "आधिकारिक खुदरा साइटें",
    weatherAdvisory: "मौसम और सलाह",
    currentWeather: "वर्तमान मौसम",
    forecast: "5-दिन का पूर्वानुमान",
    agriAdvisory: "कृषि सलाह",
    humidity: "आर्द्रता",
    wind: "हवा",
    advisoryHot: "गर्म और धूप वाले मौसम की उम्मीद है। खड़ी फसलों के लिए पर्याप्त सिंचाई सुनिश्चित करें, खासकर दोपहर के चरम घंटों के दौरान। पशुओं में गर्मी के तनाव के संकेतों की जाँच करें।",
    advisoryRain: "बारिश की उम्मीद है। खेतों में उचित जल निकासी सुनिश्चित करें ताकि जलभराव को रोका जा सके। बारिश के बाद तक उर्वरकों या कीटनाशकों के प्रयोग को स्थगित करें।",
    advisoryMixed: "मौसम में बादल छाए रहने के साथ परिवर्तनशील रहने की उम्मीद है। आर्द्र परिस्थितियों में पनपने वाले कीटों और बीमारियों के लिए फसलों की निगरानी करें। यह निराई जैसे अंतर-सांस्कृतिक कार्यों के लिए एक अच्छा समय है।",
    marketPrices: "बाजार मूल्य",
    selectState: "राज्य चुनें",
    selectDistrict: "जिला चुनें",
    searchForProduct: "उत्पाद खोजें...",
    product: "उत्पाद",
    category: "श्रेणी",
    price: "मूल्य (प्रति क्विंटल)",
    noPrices: "कीमतें देखने के लिए कृपया राज्य और जिला चुनें।",
    loading: "कीमतें लोड हो रही हैं...",
  },
  mr: {
    home: "मुख्यपृष्ठ",
    schemes: "योजना",
    products: "उत्पाद",
    learning: "शिकणे",
    awards: "पुरस्कार",
    demand: "बाजार मागणी",
    certification: "प्रमाणीकरण",
    scanner: "एआय स्कॅनर",
    weather: "हवामान",
    login: "लॉगिन",
    register: "नोंदणी करा",
    logout: "लॉगआउट",
    welcome: "ऑरगॅनिक फार्म हबमध्ये आपले स्वागत आहे!",
    tagline: "शाश्वत शेतीसाठी आपले वन-स्टॉप सोल्यूशन.",
    aboutUs: "आमच्याबद्दल",
    aboutUsContent: "ऑरगॅनिक फार्म हब सेंद्रिय शेती पद्धतींना प्रोत्साहन देण्यासाठी, शेतकऱ्यांना संसाधनांशी जोडण्यासाठी आणि ग्राहकांना निरोगी, सेंद्रिय उत्पादनांपर्यंत पोहोच देण्यासाठी समर्पित आहे. निरोगी ग्रह आणि समृद्ध शेती समुदायांसाठी एक शाश्वत कृषी परिसंस्था निर्माण करणे हे आमचे ध्येय आहे.",
    govSchemes: "सरकारी योजना",
    generalFarmerSchemes: "सर्वसाधारण शेतकरी कल्याण योजना",
    autonomousBodies: "स्वायत्त सरकारी संस्था आणि सहाय्यक संस्था",
    privateSchemes: "खाजगी उपक्रम",
    schemeTitle: "योजनेचे नाव",
    schemeDesc: "वर्णन",
    schemeEligibility: "पात्रता",
    schemeBenefits: "फायदे",
    schemeLink: "अधिक माहिती",
    productCatalog: "सेंद्रिय उत्पादने कॅटलॉग",
    searchProduct: "उत्पादन शोधा...",
    comparePrices: "किमतींची तुलना करा",
    bestPrice: "सर्वोत्तम किंमत!",
    loadingPrices: "किमती लोड होत आहेत...",
    priceError: "किमती मिळवता आल्या नाहीत. कृपया नंतर पुन्हा प्रयत्न करा.",
    learningResources: "शिकण्याची आणि अभ्यास सामग्री",
    studyMaterials: "अभ्यास सामग्री",
    youtubeVideos: "यूट्यूब व्हिडिओ",
    beginnerGuides: "नवशिक्यांसाठी मार्गदर्शक",
    advancedTopics: "प्रगत विषय",
    universityCourses: "विद्यापीठाचे अभ्यासक्रम",
    govPublications: "सरकारी प्रकाशने",
    awardsRecognition: "पुरस्कार आणि ओळख",
    nationalAwards: "राष्ट्रीय पुरस्कार",
    internationalAwards: "आंतरराष्ट्रीय पुरस्कार",
    awardName: "पुरस्काराचे नाव",
    awardOrg: "आयोजक संस्था",
    awardYear: "वर्ष",
    awardWinners: "विजेते/प्राप्तकर्ते",
    marketDemand: "बाजार मागणी आणि ट्रेंड",
    demandOverview: "एकूण बाजार मागणी",
    componentDemand: "घटक मागणी",
    demandMap: "मागणी वितरण नकाशा (भारत)",
    mapDisclaimer: "मागणी डेटा सूचक आहे आणि उपलब्ध बाजार संशोधनावर आधारित आहे. अचूक आकडेवारीसाठी, अधिकृत अहवाल पहा.",
    aiScanner: "एआय-शक्तीवर चालणारा स्कॅनर",
    uploadImage: "प्रतिमा अपलोड करा",
    scan: "निदानासाठी स्कॅन करा",
    scannerPlaceholder: "एआय-शक्तीवर चालणाऱ्या निदानासाठी आणि सेंद्रिय उपायांसाठी आपल्या वनस्पतीची किंवा कीटकाची प्रतिमा अपलोड करा.",
    scanning: "स्कॅन करत आहे...",
    scannerResult: "एआय निदान परिणाम",
    noImage: "कृपया स्कॅन करण्यासाठी प्रतिमा अपलोड करा.",
    certificationInfo: "सेंद्रिय प्रमाणीकरण आणि परीक्षा",
    certGov: "सरकारी प्रमाणीकरण",
    certPrivate: "खाजगी प्रमाणीकरण",
    certExamModule: "प्रमाणीकरण परीक्षा मॉड्यूल (सराव)",
    uploadCertificates: "आपले प्रमाणपत्र अपलोड करा (7/12, 8A)",
    email: "ईमेल",
    password: "पासवर्ड",
    farmerId: "सरकारी शेतकरी आयडी",
    upload: "अपलोड करा",
    fileUploadDisclaimer: "कृपया डिजिटल स्वाक्षरी केलेल्या प्रती अपलोड करा. हे केवळ आमच्या प्लॅटफॉर्मवर आपल्या नोंदी ठेवण्यासाठी आहे. अधिकृत पडताळणीसाठी सरकारी पोर्टलची आवश्यकता आहे.",
    fileUploaded: "फाइल यशस्वीरित्या अपलोड झाली!",
    loginSuccess: "लॉगिन यशस्वी!",
    loginFailed: "अवैध ईमेल किंवा पासवर्ड.",
    registerSuccess: "नोंदणी यशस्वी! कृपया लॉगिन करा।",
    registerFailed: "नोंदणी अयशस्वी झाली. कृपया पुन्हा प्रयत्न करा.",
    emailRequired: "ईमेल आवश्यक आहे.",
    passwordRequired: "पासवर्ड आवश्यक आहे.",
    invalidEmail: "अवैध ईमेल स्वरूप.",
    passwordMinLength: "पासवर्ड किमान 6 वर्णांचा असावा.",
    farmerIdOptional: "शेतकरी आयडी (लिंक करण्यासाठी पर्यायी, पासवर्ड म्हणून नाही)",
    confirmPassword: "पासवर्डची पुष्टी करा",
    passwordsMismatch: "पासवर्ड जुळत नाहीत.",
    requiredField: "हे क्षेत्र आवश्यक आहे.",
    viewProfile: "प्रोफाइल पहा",
    upload712: "7/12 उतारा अपलोड करा",
    upload8A: "8A उतारा अपलोड करा",
    userDocuments: "आपली अपलोड केलेली कागदपत्रे",
    noDocuments: "अद्याप कोणतीही कागदपत्रे अपलोड केलेली नाहीत.",
    documentType: "कागदपत्राचा प्रकार",
    fileName: "फाइलचे नाव",
    uploadedOn: "यावर अपलोड केले",
    status: "स्थिती",
    pending: "पडताळणी प्रलंबित",
    verified: "पडताळणी झाली",
    download: "डाउनलोड करा",
    contactUs: "आमच्याशी संपर्क साधा",
    contactInfo: "कोणत्याही प्रश्नांसाठी, कृपया आमच्याशी संपर्क साधा:",
    emailAddress: "suyashmule16@gmail.com",
    phoneNumber: "+91 8468846995",
    yourName: "तुमचे नाव",
    subject: "विषय",
    message: "संदेश",
    sendMessage: "संदेश पाठवा",
    messageSentSuccess: "तुमच्या संदेशाबद्दल धन्यवाद! आम्ही लवकरच तुमच्याशी संपर्क साधू.",
    messageSentError: "संदेश पाठवण्यात अयशस्वी. कृपया नंतर पुन्हा प्रयत्न करा.",
    followUs: "आम्हाला फॉलो करा",
    footerText: "© 2025 ऑरगॅनिक फार्म हब. सर्व हक्क राखीव.",
    visitYouTube: "अधिक व्हिडिओंसाठी यूट्यूबला भेट द्या",
    onlineCourses: "ऑनलाइन प्रमाणपत्र अभ्यासक्रम आणि संसाधने",
    updatePrices: "किमती अपडेट करा",
    officialSites: "अधिकृत किरकोळ साइट्स",
    weatherAdvisory: "हवामान आणि सल्ला",
    currentWeather: "सध्याचे हवामान",
    forecast: "5-दिवसांचा अंदाज",
    agriAdvisory: "कृषी सल्ला",
    humidity: "आर्द्रता",
    wind: "वारा",
    advisoryHot: "गरम आणि सूर्यप्रकाशाची स्थिती अपेक्षित आहे. उभ्या पिकांसाठी पुरेसे सिंचन सुनिश्चित करा, विशेषतः दुपारच्या वेळी. पशुधनातील उष्णतेच्या तणावाची चिन्हे तपासा.",
    advisoryRain: "पावसाची अपेक्षा आहे. शेतात योग्य निचरा सुनिश्चित करा जेणेकरून पाणी साचणार नाही. पाऊस पडून गेल्यानंतर खते किंवा कीटकनाशकांची फवारणी पुढे ढकला.",
    advisoryMixed: "ढगाळ हवामानासह हवामान बदलणारे राहण्याची शक्यता आहे. दमट परिस्थितीत वाढणाऱ्या कीड आणि रोगांसाठी पिकांचे निरीक्षण करा. तण काढण्यासारख्या आंतरमशागत कामांसाठी हा चांगला काळ आहे.",
    marketPrices: "बाजार भाव",
    selectState: "राज्य निवडा",
    selectDistrict: "जिल्हा निवडा",
    searchForProduct: "उत्पादन शोधा...",
    product: "उत्पादन",
    category: "श्रेणी",
    price: "किंमत (प्रति क्विंटल)",
    noPrices: "भाव पाहण्यासाठी कृपया राज्य आणि जिल्हा निवडा.",
    loading: "भाव लोड होत आहेत...",
  }
};

// --- New Location & Product Data ---
const indiaStates = {
  "Andhra Pradesh": ["Anantapur", "Chittoor", "East Godavari", "Guntur", "Krishna", "Kurnool", "Prakasam", "Srikakulam", "Visakhapatnam", "Vizianagaram", "West Godavari", "YSR Kadapa"],
  "Arunachal Pradesh": ["Tawang", "West Kameng", "East Kameng", "Papum Pare", "Kurung Kumey", "Kra Daadi", "Lower Subansiri", "Upper Subansiri", "West Siang", "East Siang", "Siang", "Upper Siang", "Lower Siang", "Lower Dibang Valley", "Dibang Valley", "Anjaw", "Lohit", "Namsai", "Changlang", "Tirap", "Longding"],
  "Assam": ["Baksa", "Barpeta", "Biswanath", "Bongaigaon", "Cachar", "Charaideo", "Chirang", "Darrang", "Dhemaji", "Dhubri", "Dibrugarh", "Goalpara", "Golaghat", "Hailakandi", "Hojai", "Jorhat", "Kamrup Metropolitan", "Kamrup", "Karbi Anglong", "Karimganj", "Kokrajhar", "Lakhimpur", "Majuli", "Morigaon", "Nagaon", "Nalbari", "Dima Hasao", "Sivasagar", "Sonitpur", "South Salmara-Mankachar", "Tinsukia", "Udalguri", "West Karbi Anglong"],
  "Bihar": ["Araria", "Arwal", "Aurangabad", "Banka", "Begusarai", "Bhagalpur", "Bhojpur", "Buxar", "Darbhanga", "East Champaran (Motihari)", "Gaya", "Gopalganj", "Jamui", "Jehanabad", "Kaimur (Bhabua)", "Katihar", "Khagaria", "Kishanganj", "Lakhisarai", "Madhepura", "Madhubani", "Munger (Monghyr)", "Muzaffarpur", "Nalanda", "Nawada", "Patna", "Purnia (Purnea)", "Rohtas", "Saharsa", "Samastipur", "Saran", "Sheikhpura", "Sheohar", "Sitamarhi", "Siwan", "Supaul", "Vaishali", "West Champaran"],
  "Chhattisgarh": ["Balod", "Baloda Bazar", "Balrampur", "Bastar", "Bemetara", "Bijapur", "Bilaspur", "Dantewada (South Bastar)", "Dhamtari", "Durg", "Gariyaband", "Janjgir-Champa", "Jashpur", "Kabirdham (Kawardha)", "Kanker (North Bastar)", "Kondagaon", "Korba", "Koriya", "Mahasamund", "Mungeli", "Narayanpur", "Raigarh", "Raipur", "Rajnandgaon", "Sukma", "Surajpur", "Surguja"],
  "Goa": ["North Goa", "South Goa"],
  "Gujarat": ["Ahmedabad", "Amreli", "Anand", "Aravalli", "Banaskantha (Palanpur)", "Bharuch", "Bhavnagar", "Botad", "Chhota Udepur", "Dahod", "Dangs (Ahwa)", "Devbhoomi Dwarka", "Gandhinagar", "Gir Somnath", "Jamnagar", "Junagadh", "Kachchh", "Kheda (Nadiad)", "Mahisagar", "Mehsana", "Morbi", "Narmada (Rajpipla)", "Navsari", "Panchmahal (Godhra)", "Patan", "Porbandar", "Rajkot", "Sabarkantha (Himmatnagar)", "Surat", "Surendranagar", "Tapi (Vyara)", "Vadodara", "Valsad"],
  "Haryana": ["Ambala", "Bhiwani", "Charkhi Dadri", "Faridabad", "Fatehabad", "Gurugram (Gurgaon)", "Hisar", "Jhajjar", "Jind", "Kaithal", "Karnal", "Kurukshetra", "Mahendragarh", "Nuh", "Palwal", "Panchkula", "Panipat", "Rewari", "Rohtak", "Sirsa", "Sonipat", "Yamunanagar"],
  "Himachal Pradesh": ["Bilaspur", "Chamba", "Hamirpur", "Kangra", "Kinnaur", "Kullu", "Lahaul & Spiti", "Mandi", "Shimla", "Sirmaur (Sirmour)", "Solan", "Una"],
  "Jharkhand": ["Bokaro", "Chatra", "Deoghar", "Dhanbad", "Dumka", "East Singhbhum", "Garhwa", "Giridih", "Godda", "Gumla", "Hazaribag", "Jamtara", "Khunti", "Koderma", "Latehar", "Lohardaga", "Pakur", "Palamu", "Ramgarh", "Ranchi", "Sahebganj", "Seraikela-Kharsawan", "Simdega", "West Singhbhum"],
  "Karnataka": ["Bagalkot", "Ballari (Bellary)", "Belagavi (Belgaum)", "Bengaluru (Bangalore) Rural", "Bengaluru (Bangalore) Urban", "Bidar", "Chamarajanagar", "Chikballapur", "Chikkamagaluru (Chikmagalur)", "Chitradurga", "Dakshina Kannada", "Davangere", "Dharwad", "Gadag", "Hassan", "Haveri", "Kalaburagi (Gulbarga)", "Kodagu", "Kolar", "Koppal", "Mandya", "Mysuru (Mysore)", "Raichur", "Ramanagara", "Shivamogga (Shimoga)", "Tumakuru (Tumkur)", "Udupi", "Uttara Kannada (Karwar)", "Vijayapura (Bijapur)", "Yadgir"],
  "Kerala": ["Alappuzha", "Ernakulam", "Idukki", "Kannur", "Kasaragod", "Kollam", "Kottayam", "Kozhikode", "Malappuram", "Palakkad", "Pathanamthitta", "Thiruvananthapuram", "Thrissur", "Wayanad"],
  "Madhya Pradesh": ["Agar Malwa", "Alirajpur", "Anuppur", "Ashoknagar", "Balaghat", "Barwani", "Betul", "Bhind", "Bhopal", "Burhanpur", "Chhatarpur", "Chhindwara", "Damoh", "Datia", "Dewas", "Dhar", "Dindori", "Guna", "Gwalior", "Harda", "Hoshangabad", "Indore", "Jabalpur", "Jhabua", "Katni", "Khandwa", "Khargone", "Mandla", "Mandsaur", "Morena", "Narsinghpur", "Neemuch", "Panna", "Raisen", "Rajgarh", "Ratlam", "Rewa", "Sagar", "Satna", "Sehore", "Seoni", "Shahdol", "Shajapur", "Sheopur", "Shivpuri", "Sidhi", "Singrauli", "Tikamgarh", "Ujjain", "Umaria", "Vidisha"],
  "Maharashtra": ["Ahmednagar", "Akola", "Amravati", "Aurangabad", "Beed", "Bhandara", "Buldhana", "Chandrapur", "Dhule", "Gadchiroli", "Gondia", "Hingoli", "Jalgaon", "Jalna", "Kolhapur", "Latur", "Mumbai City", "Mumbai Suburban", "Nagpur", "Nanded", "Nandurbar", "Nashik", "Osmanabad", "Palghar", "Parbhani", "Pune", "Raigad", "Ratnagiri", "Sangli", "Satara", "Sindhudurg", "Solapur", "Thane", "Wardha", "Washim", "Yavatmal"],
  "Manipur": ["Bishnupur", "Chandel", "Churachandpur", "Imphal East", "Imphal West", "Jiribam", "Kakching", "Kamjong", "Kangpokpi", "Noney", "Pherzawl", "Senapati", "Tamenglong", "Tengnoupal", "Thoubal", "Ukhrul"],
  "Meghalaya": ["East Garo Hills", "East Jaintia Hills", "East Khasi Hills", "North Garo Hills", "Ri Bhoi", "South Garo Hills", "South West Garo Hills", "South West Khasi Hills", "West Garo Hills", "West Jaintia Hills", "West Khasi Hills"],
  "Mizoram": ["Aizawl", "Champhai", "Hnahthial", "Khawzawl", "Kolasib", "Lawngtlai", "Lunglei", "Mamit", "Saiha", "Saitual", "Serchhip"],
  "Nagaland": ["Dimapur", "Kiphire", "Kohima", "Longleng", "Mokokchung", "Mon", "Peren", "Phek", "Tuensang", "Wokha", "Zunheboto"],
  "Odisha": ["Angul", "Balangir", "Balasore", "Bargarh", "Bhadrak", "Boudh", "Cuttack", "Deogarh", "Dhenkanal", "Gajapati", "Ganjam", "Jagatsinghpur", "Jajpur", "Jharsuguda", "Kalahandi", "Kandhamal", "Kendrapara", "Kendujhar (Keonjhar)", "Khordha", "Koraput", "Malkangiri", "Mayurbhanj", "Nabarangpur", "Nayagarh", "Nuapada", "Puri", "Rayagada", "Sambalpur", "Sonepur", "Sundargarh"],
  "Punjab": ["Amritsar", "Barnala", "Bathinda", "Faridkot", "Fatehgarh Sahib", "Fazilka", "Ferozepur", "Gurdaspur", "Hoshiarpur", "Jalandhar", "Kapurthala", "Ludhiana", "Mansa", "Moga", "Muktsar", "Nawanshahr (Shahid Bhagat Singh Nagar)", "Pathankot", "Patiala", "Rupnagar", "Sahibzada Ajit Singh Nagar (Mohali)", "Sangrur", "Tarn Taran"],
  "Rajasthan": ["Ajmer", "Alwar", "Banswara", "Baran", "Barmer", "Bharatpur", "Bhilwara", "Bikaner", "Bundi", "Chittorgarh", "Churu", "Dausa", "Dholpur", "Dungarpur", "Hanumangarh", "Jaipur", "Jaisalmer", "Jalore", "Jhalawar", "Jhunjhunu", "Jodhpur", "Karauli", "Kota", "Nagaur", "Pali", "Pratapgarh", "Rajsamand", "Sawai Madhopur", "Sikar", "Sirohi", "Sri Ganganagar", "Tonk", "Udaipur"],
  "Sikkim": ["East Sikkim", "North Sikkim", "South Sikkim", "West Sikkim"],
  "Tamil Nadu": ["Ariyalur", "Chengalpattu", "Chennai", "Coimbatore", "Cuddalore", "Dharmapuri", "Dindigul", "Erode", "Kallakurichi", "Kanchipuram", "Kanyakumari", "Karur", "Krishnagiri", "Madurai", "Mayiladuthurai", "Nagapattinam", "Namakkal", "Nilgiris", "Perambalur", "Pudukkottai", "Ramanathapuram", "Ranipet", "Salem", "Sivaganga", "Tenkasi", "Thanjavur", "Theni", "Thoothukudi (Tuticorin)", "Tiruchirappalli", "Tirunelveli", "Tirupathur", "Tiruppur", "Tiruvallur", "Tiruvannamalai", "Tiruvarur", "Vellore", "Viluppuram", "Virudhunagar"],
  "Telangana": ["Adilabad", "Bhadradri Kothagudem", "Hyderabad", "Jagtial", "Jangaon", "Jayashankar Bhupalpally", "Jogulamba Gadwal", "Kamareddy", "Karimnagar", "Khammam", "Komaram Bheem Asifabad", "Mahabubabad", "Mahabubnagar", "Mancherial", "Medak", "Medchal", "Mulugu", "Nagarkurnool", "Nalgonda", "Narayanpet", "Nirmal", "Nizamabad", "Peddapalli", "Rajanna Sircilla", "Rangareddy", "Sangareddy", "Siddipet", "Suryapet", "Vikarabad", "Wanaparthy", "Warangal (Rural)", "Warangal (Urban)", "Yadadri Bhuvanagiri"],
  "Tripura": ["Dhalai", "Gomati", "Khowai", "North Tripura", "Sepahijala", "South Tripura", "Unakoti", "West Tripura"],
  "Uttar Pradesh": ["Agra", "Aligarh", "Allahabad", "Ambedkar Nagar", "Amethi (Chatrapati Sahuji Mahraj Nagar)", "Amroha (J.P. Nagar)", "Auraiya", "Azamgarh", "Baghpat", "Bahraich", "Ballia", "Balrampur", "Banda", "Barabanki", "Bareilly", "Basti", "Bhadohi", "Bijnor", "Budaun", "Bulandshahr", "Chandauli", "Chitrakoot", "Deoria", "Etah", "Etawah", "Faizabad", "Farrukhabad", "Fatehpur", "Firozabad", "Gautam Buddha Nagar", "Ghaziabad", "Ghazipur", "Gonda", "Gorakhpur", "Hamirpur", "Hapur (Panchsheel Nagar)", "Hardoi", "Hathras", "Jalaun", "Jaunpur", "Jhansi", "Kannauj", "Kanpur Dehat", "Kanpur Nagar", "Kasganj (Kanshiram Nagar)", "Kaushambi", "Kushinagar (Padrauna)", "Lakhimpur - Kheri", "Lalitpur", "Lucknow", "Maharajganj", "Mahoba", "Mainpuri", "Mathura", "Mau", "Meerut", "Mirzapur", "Moradabad", "Muzaffarnagar", "Pilibhit", "Pratapgarh", "RaeBareli", "Rampur", "Saharanpur", "Sambhal (Bhim Nagar)", "Sant Kabir Nagar", "Shahjahanpur", "Shamli", "Shravasti", "Siddharth Nagar", "Sitapur", "Sonbhadra", "Sultanpur", "Unnao", "Varanasi"],
  "Uttarakhand": ["Almora", "Bageshwar", "Chamoli", "Champawat", "Dehradun", "Haridwar", "Nainital", "Pauri Garhwal", "Pithoragarh", "Rudraprayag", "Tehri Garhwal", "Udham Singh Nagar", "Uttarkashi"],
  "West Bengal": ["Alipurduar", "Bankura", "Birbhum", "Cooch Behar", "Dakshin Dinajpur (South Dinajpur)", "Darjeeling", "Hooghly", "Howrah", "Jalpaiguri", "Jhargram", "Kalimpong", "Kolkata", "Malda", "Murshidabad", "Nadia", "North 24 Parganas", "Paschim Medinipur (West Medinipur)", "Paschim (West) Burdwan", "Purba Burdwan (Bardhaman)", "Purba Medinipur (East Medinipur)", "Purulia", "South 24 Parganas", "Uttar Dinajpur (North Dinajpur)"]
};

const farmProducts = [
  // Cereals / Grains
  { name: "Wheat", category: "Cereals / Grains" },
  { name: "Rice", category: "Cereals / Grains" },
  { name: "Maize (Corn)", category: "Cereals / Grains" },
  { name: "Barley", category: "Cereals / Grains" },
  { name: "Millet (Bajra)", category: "Cereals / Grains" },
  { name: "Sorghum (Jowar)", category: "Cereals / Grains" },
  { name: "Oats", category: "Cereals / Grains" },
  // Pulses / Legumes
  { name: "Lentils (Masoor)", category: "Pulses / Legumes" },
  { name: "Chickpeas (Chana)", category: "Pulses / Legumes" },
  { name: "Pigeon Peas (Arhar/Tur)", category: "Pulses / Legumes" },
  { name: "Mung Beans (Moong)", category: "Pulses / Legumes" },
  { name: "Black Gram (Urad)", category: "Pulses / Legumes" },
  { name: "Kidney Beans (Rajma)", category: "Pulses / Legumes" },
  { name: "Soybeans", category: "Pulses / Legumes" },
  // Vegetables
  { name: "Potato", category: "Vegetables" },
  { name: "Tomato", category: "Vegetables" },
  { name: "Onion", category: "Vegetables" },
  { name: "Garlic", category: "Vegetables" },
  { name: "Ginger", category: "Vegetables" },
  { name: "Carrot", category: "Vegetables" },
  { name: "Cabbage", category: "Vegetables" },
  { name: "Cauliflower", category: "Vegetables" },
  { name: "Spinach", category: "Vegetables" },
  { name: "Eggplant (Brinjal)", category: "Vegetables" },
  { name: "Okra (Lady Finger)", category: "Vegetables" },
  { name: "Green Chilli", category: "Vegetables" },
  // Fruits
  { name: "Apple", category: "Fruits" },
  { name: "Banana", category: "Fruits" },
  { name: "Mango", category: "Fruits" },
  { name: "Orange", category: "Fruits" },
  { name: "Papaya", category: "Fruits" },
  { name: "Pineapple", category: "Fruits" },
  { name: "Grapes", category: "Fruits" },
  { name: "Watermelon", category: "Fruits" },
  // Oilseeds
  { name: "Groundnut (Peanut)", category: "Oilseeds" },
  { name: "Mustard", category: "Oilseeds" },
  { name: "Sunflower", category: "Oilseeds" },
  { name: "Sesame (Til)", category: "Oilseeds" },
  // Spices & Condiments
  { name: "Turmeric", category: "Spices & Condiments" },
  { name: "Black Pepper", category: "Spices & Condiments" },
  { name: "Cumin", category: "Spices & Condiments" },
  { name: "Coriander", category: "Spices & Condiments" },
  // Sugar Crops
  { name: "Sugarcane", category: "Sugar Crops" },
  // Fiber Crops
  { name: "Cotton", category: "Fiber Crops" },
  // Fodder / Forage Crops
  { name: "Alfalfa", category: "Fodder / Forage Crops" },
];

// --- Dummy Data ---
const dummySchemes = [
  {
    id: 1,
    title: { en: "Paramparagat Krishi Vikas Yojana (PKVY)", hi: "परंपरागत कृषि विकास योजना (पीकेवीवाय)", mr: "परंपरागत कृषि विकास योजना (पीकेव्हीवाय)" },
    description: { en: "A scheme to promote organic farming through cluster approach and Participatory Guarantee System (PGS).", hi: "क्लस्टर दृष्टिकोण और भागीदारी गारंटी प्रणाली (पीजीएस) के माध्यम से जैविक खेती को बढ़ावा देने की योजना।", mr: "क्लस्टर दृष्टिकोन आणि सहभागात्मक हमी प्रणाली (पीजीएस) द्वारे सेंद्रिय शेतीला प्रोत्साहन देण्यासाठी योजना." },
    eligibility: { en: "Farmers organized into clusters of 20 hectares or more.", hi: "20 हेक्टेयर या उससे अधिक के समूहों में संगठित किसान।", mr: "20 हेक्टर किंवा त्याहून अधिक क्षेत्राच्या समूहांमध्ये संघटित शेतकरी." },
    benefits: { en: "Financial assistance, training, and certification support.", hi: "वित्तीय सहायता, प्रशिक्षण और प्रमाणीकरण सहायता।", mr: "आर्थिक सहाय्य, प्रशिक्षण आणि प्रमाणीकरण समर्थन." },
    link: "https://www.myscheme.gov.in/schemes/pkvy"
  },
  {
    id: 2,
    title: { en: "Mission Organic Value Chain Development for North Eastern Region (MOVCDNER)", hi: "पूर्वोत्तर क्षेत्र के लिए मिशन ऑर्गेनिक वैल्यू चेन डेवलपमेंट (एमओवीसीडीएनईआर)", mr: "ईशान्येकडील प्रदेशासाठी मिशन ऑरगॅनिक व्हॅल्यू चेन डेव्हलपमेंट (एमओव्हीसीडीएनईआर)" },
    description: { en: "Aims to develop certified organic production in the North Eastern Region.", hi: "पूर्वोत्तर क्षेत्र में प्रमाणित जैविक उत्पादन विकसित करने का लक्ष्य है।", mr: "ईशान्येकडील प्रदेशात प्रमाणित सेंद्रिय उत्पादन विकसित करण्याचे उद्दिष्ट आहे." },
    eligibility: { en: "Farmers in North Eastern states.", hi: "पूर्वोत्तर राज्यों के किसान।", mr: "ईशान्येकडील राज्यांमधील शेतकरी." },
    benefits: { en: "End-to-end support from production to marketing.", hi: "उत्पादन से विपणन तक एंड-टू-एंड समर्थन।", mr: "उत्पादनापासून विपणनापर्यंत एंड-टू-एंड समर्थन." },
    link: "https://apeda.gov.in/apedawebsite/organic/movcdner.htm"
  }
];

const dummyGeneralFarmerSchemes = [
    {
        id: 1,
        title: { en: "Pradhan Mantri Kisan Samman Nidhi (PM-KISAN)", hi: "प्रधानमंत्री किसान सम्मान निधि (पीएम-किसान)", mr: "प्रधानमंत्री किसान सन्मान निधी (पीएम-किसान)" },
        description: { en: "Provides income support of ₹6,000 per year in three equal installments to all landholding farmer families.", hi: "सभी भूमिधारक किसान परिवारों को तीन समान किस्तों में प्रति वर्ष ₹6,000 की आय सहायता प्रदान करता है।", mr: "सर्व जमीनधारक शेतकरी कुटुंबांना तीन समान हप्त्यांमध्ये प्रति वर्ष ₹6,000 ची उत्पन्न मदत प्रदान करते." },
        eligibility: { en: "All landholding farmer families.", hi: "सभी भूमिधारक किसान परिवार।", mr: "सर्व जमीनधारक शेतकरी कुटुंबे." },
        benefits: { en: "₹6,000 per year.", hi: "प्रति वर्ष ₹6,000।", mr: "प्रति वर्ष ₹6,000." },
        link: "https://pmkisan.gov.in/"
    },
    {
        id: 2,
        title: { en: "Pradhan Mantri Fasal Bima Yojana (PMFBY)", hi: "प्रधानमंत्री फसल बीमा योजना (पीएमएफबीवाई)", mr: "प्रधानमंत्री फसल विमा योजना (पीएमएफबीवाय)" },
        description: { en: "An insurance service for farmers for their yields, providing financial support for crop loss/damage from unforeseen events.", hi: "किसानों को उनकी उपज के लिए एक बीमा सेवा, जो अप्रत्याशित घटनाओं से फसल हानि/क्षति के लिए वित्तीय सहायता प्रदान करती है।", mr: "शेतकऱ्यांसाठी त्यांच्या उत्पन्नासाठी एक विमा सेवा, जी अनपेक्षित घटनांमुळे होणाऱ्या पीक नुकसानीसाठी आर्थिक सहाय्य प्रदान करते." },
        eligibility: { en: "All farmers including sharecroppers and tenant farmers growing notified crops in notified areas.", hi: "अधिसूचित क्षेत्रों में अधिसूचित फसलें उगाने वाले सभी किसान, जिनमें बटाईदार और काश्तकार किसान शामिल हैं।", mr: "अधिसूचित क्षेत्रांमध्ये अधिसूचित पिके घेणारे सर्व शेतकरी, भाडेकरू आणि कुळांचे शेतकरी." },
        benefits: { en: "Insurance cover against crop failure.", hi: "फसल विफलता के खिलाफ बीमा कवर।", mr: "पीक अपयशाविरुद्ध विमा संरक्षण." },
        link: "https://pmfby.gov.in/"
    },
    {
        id: 3,
        title: { en: "Pradhan Mantri Kisan Maandhan Yojana (PMKMY)", hi: "प्रधानमंत्री किसान मानधन योजना (पीएमकेएमवाई)", mr: "प्रधानमंत्री किसान मानधन योजना (पीएमकेएमवाय)" },
        description: { en: "A pension scheme for small and marginal farmers of the country to provide social security.", hi: "देश के छोटे और सीमांत किसानों के लिए सामाजिक सुरक्षा प्रदान करने हेतु एक पेंशन योजना।", mr: "देशातील लहान आणि अत्यल्प भूधारक शेतकऱ्यांसाठी सामाजिक सुरक्षा प्रदान करणारी एक पेन्शन योजना." },
        eligibility: { en: "Small and Marginal Farmers (SMF) aged 18-40.", hi: "18-40 आयु वर्ग के छोटे और सीमांत किसान (एसएमएफ)।", mr: "18-40 वयोगटातील लहान आणि अत्यल्प भूधारक शेतकरी." },
        benefits: { en: "Monthly pension of ₹3,000 on attaining the age of 60.", hi: "60 वर्ष की आयु प्राप्त करने पर ₹3,000 की मासिक पेंशन।", mr: "वयाची 60 वर्षे पूर्ण झाल्यावर ₹3,000 मासिक पेन्शन." },
        link: "https://pmkmy.gov.in/"
    },
    {
        id: 4,
        title: { en: "PM-KUSUM Scheme", hi: "पीएम-कुसुम योजना", mr: "पीएम-कुसुम योजना" },
        description: { en: "Aims to ensure energy security for farmers by promoting the use of solar energy in the agriculture sector.", hi: "कृषि क्षेत्र में सौर ऊर्जा के उपयोग को बढ़ावा देकर किसानों के लिए ऊर्जा सुरक्षा सुनिश्चित करना।", mr: "कृषी क्षेत्रात सौर ऊर्जेचा वापर वाढवून शेतकऱ्यांसाठी ऊर्जा सुरक्षा सुनिश्चित करणे." },
        eligibility: { en: "Individual farmers, groups of farmers, cooperatives, etc.", hi: "व्यक्तिगत किसान, किसानों के समूह, सहकारी समितियां, आदि।", mr: "वैयक्तिक शेतकरी, शेतकऱ्यांचे गट, सहकारी संस्था इत्यादी." },
        benefits: { en: "Subsidy on solar pumps and grid-connected solar power plants.", hi: "सोलर पंप और ग्रिड से जुड़े सोलर पावर प्लांट पर सब्सिडी।", mr: "सौर पंप आणि ग्रीडला जोडलेल्या सौर ऊर्जा प्रकल्पांवर अनुदान." },
        link: "https://mnre.gov.in/"
    },
    {
        id: 5,
        title: { en: "PM Kisan Credit Card (PM-KCC)", hi: "पीएम किसान क्रेडिट कार्ड (पीएम-केसीसी)", mr: "पीएम किसान क्रेडिट कार्ड (पीएम-केसीसी)" },
        description: { en: "Provides adequate and timely credit support from the banking system to farmers for their cultivation and other needs.", hi: "किसानों को उनकी खेती और अन्य जरूरतों के लिए बैंकिंग प्रणाली से पर्याप्त और समय पर ऋण सहायता प्रदान करता है।", mr: "शेतकऱ्यांना त्यांच्या शेती आणि इतर गरजांसाठी बँकिंग प्रणालीकडून पुरेशी आणि वेळेवर पतपुरवठा करते." },
        eligibility: { en: "Farmers, animal husbandry and fisheries farmers.", hi: "किसान, पशुपालन और मत्स्य पालन किसान।", mr: "शेतकरी, पशुसंवर्धन आणि मत्स्यपालक शेतकरी." },
        benefits: { en: "Access to credit at a lower interest rate.", hi: "कम ब्याज दर पर ऋण की सुविधा।", mr: "कमी व्याजदराने पतपुरवठा." },
        link: "https://fw.pmkisan.gov.in/Kcc/Main.aspx"
    },
     {
        id: 6,
        title: { en: "MahaDBT Portal (Maharashtra)", hi: "महाडीबीटी पोर्टल (महाराष्ट्र)", mr: "महाडीबीटी पोर्टल (महाराष्ट्र)" },
        description: { en: "A portal by the Government of Maharashtra for direct benefit transfer for various farmer schemes within the state.", hi: "राज्य के भीतर विभिन्न किसान योजनाओं के लिए प्रत्यक्ष लाभ हस्तांतरण के लिए महाराष्ट्र सरकार का एक पोर्टल।", mr: "राज्यातील विविध शेतकरी योजनांसाठी थेट लाभ हस्तांतरणासाठी महाराष्ट्र सरकारचे एक पोर्टल." },
        eligibility: { en: "Farmers residing in Maharashtra.", hi: "महाराष्ट्र में रहने वाले किसान।", mr: "महाराष्ट्रात राहणारे शेतकरी." },
        benefits: { en: "Direct transfer of subsidies for various agricultural schemes.", hi: "विभिन्न कृषि योजनाओं के लिए सब्सिडी का सीधा हस्तांतरण।", mr: "विविध कृषी योजनांसाठी अनुदानाचे थेट हस्तांतरण." },
        link: "https://mahadbt.maharashtra.gov.in/"
    },
    {
        id: 7,
        title: { en: "Rythu Bandhu Scheme (Telangana)", hi: "रायथु बंधु योजना (तेलंगाना)", mr: "रायथू बंधू योजना (तेलंगणा)" },
        description: { en: "Telangana government's investment support scheme providing financial assistance to farmers for two crops a year.", hi: "तेलंगाना सरकार की निवेश सहायता योजना जो किसानों को साल में दो फसलों के लिए वित्तीय सहायता प्रदान करती है।", mr: "तेलंगणा सरकारची गुंतवणूक सहाय्य योजना जी शेतकऱ्यांना वर्षातून दोन पिकांसाठी आर्थिक सहाय्य प्रदान करते." },
        eligibility: { en: "All land-owning farmers in Telangana.", hi: "तेलंगाना में सभी भूमि-स्वामी किसान।", mr: "तेलंगणातील सर्व जमीन मालक शेतकरी." },
        benefits: { en: "₹5,000 per acre per season.", hi: "₹5,000 प्रति एकड़ प्रति मौसम।", mr: "प्रति एकर प्रति हंगाम ₹5,000." },
        link: "https://rythubandhu.telangana.gov.in/"
    },
    {
        id: 8,
        title: { en: "Godhan Nyay Yojana (Chhattisgarh)", hi: "गोधन न्याय योजना (छत्तीसगढ़)", mr: "गोधन न्याय योजना (छत्तीसगड)" },
        description: { en: "A scheme to procure cow dung from cattle rearers at a fixed rate and convert it into vermicompost.", hi: "पशुपालकों से एक निश्चित दर पर गोबर खरीदकर उसे वर्मीकम्पोस्ट में बदलने की योजना।", mr: "पशुपालकांकडून ठराविक दराने शेण खरेदी करून त्याचे वर्मीकंपोस्टमध्ये रूपांतर करण्याची योजना." },
        eligibility: { en: "Cattle rearers in Chhattisgarh.", hi: "छत्तीसगढ़ में पशुपालक।", mr: "छत्तीसगडमधील पशुपालक." },
        benefits: { en: "Provides additional income and promotes organic farming.", hi: "अतिरिक्त आय प्रदान करता है और जैविक खेती को बढ़ावा देता है।", mr: "अतिरिक्त उत्पन्न प्रदान करते आणि सेंद्रिय शेतीला प्रोत्साहन देते." },
    link: "https://godhannyay.cgstate.gov.in/"
  }
];

const dummySupportBodies = [
    { id: 1, title: { en: "Small Farmers Agribusiness Consortium (SFAC)", hi: "लघु कृषक कृषि व्यापार संघ (एसएफएसी)", mr: "लहान शेतकरी कृषी व्यवसाय संघ (एसएफएसी)" }, description: { en: "Organizes small farmers into Producer Organizations (FPOs) to enhance their competitiveness and increase market access.", hi: "छोटे किसानों को उत्पादक संगठनों (एफपीओ) में संगठित करता है ताकि उनकी प्रतिस्पर्धात्मकता बढ़ाई जा सके और बाजार पहुंच में वृद्धि हो।", mr: "लहान शेतकऱ्यांना उत्पादक संस्थांमध्ये (एफपीओ) संघटित करून त्यांची स्पर्धात्मकता वाढवते आणि बाजारपेठेत प्रवेश वाढवते." }, link: "http://sfacindia.com/" },
    { id: 2, title: { en: "National Bank for Agriculture and Rural Development (NABARD)", hi: "राष्ट्रीय कृषि और ग्रामीण विकास बैंक (नाबार्ड)", mr: "राष्ट्रीय कृषी आणि ग्रामीण विकास बँक (नाबार्ड)" }, description: { en: "An apex development bank providing credit for agriculture and rural development, fostering rural prosperity.", hi: "कृषि और ग्रामीण विकास के लिए ऋण प्रदान करने वाला एक शीर्ष विकास बैंक, जो ग्रामीण समृद्धि को बढ़ावा देता है।", mr: "कृषी आणि ग्रामीण विकासासाठी पतपुरवठा करणारी एक सर्वोच्च विकास बँक, जी ग्रामीण समृद्धीला चालना देते." }, link: "https://www.nabard.org/" },
    { id: 3, title: { en: "Agricultural and Processed Food Products Export Development Authority (APEDA)", hi: "कृषि और प्रसंस्कृत खाद्य उत्पाद निर्यात विकास प्राधिकरण (एपीडा)", mr: "कृषी आणि प्रक्रिया केलेले अन्न उत्पादने निर्यात विकास प्राधिकरण (अपेडा)" }, description: { en: "Promotes the export of agricultural and processed food products by providing financial assistance, information, and guidelines.", hi: "वित्तीय सहायता, सूचना और दिशानिर्देश प्रदान करके कृषि और प्रसंस्कृत खाद्य उत्पादों के निर्यात को बढ़ावा देता है।", mr: "आर्थिक सहाय्य, माहिती आणि मार्गदर्शक तत्त्वे देऊन कृषी आणि प्रक्रिया केलेल्या अन्न उत्पादनांच्या निर्यातीला प्रोत्साहन देते." }, link: "https://apeda.gov.in/" },
    { id: 4, title: { en: "Central Warehousing Corporation (CWC)", hi: "केंद्रीय भंडारण निगम (सीडब्ल्यूसी)", mr: "केंद्रीय वखार महामंडळ (सीडब्ल्यूसी)" }, description: { en: "Provides scientific storage and logistics solutions for agricultural produce, industrial goods, and imported/exported items.", hi: "कृषि उपज, औद्योगिक वस्तुओं और आयातित/निर्यातित वस्तुओं के लिए वैज्ञानिक भंडारण और रसद समाधान प्रदान करता है।", mr: "कृषी उत्पादने, औद्योगिक वस्तू आणि आयात/निर्यात केलेल्या वस्तूंसाठी वैज्ञानिक साठवण आणि लॉजिस्टिक सोल्यूशन्स प्रदान करते." }, link: "https://cewacor.nic.in/" },
    { id: 5, title: { en: "Directorate of Plant Protection, Quarantine and Storage (PPQS)", hi: "पौध संरक्षण, संगरोध और भंडारण निदेशालय (पीपीक्यूएस)", mr: "वनस्पती संरक्षण, संगरोध आणि साठवण संचालनालय (पीपीक्यूएस)" }, description: { en: "Prevents the introduction and spread of exotic pests in India and facilitates safe global trade in agricultural commodities.", hi: "भारत में विदेशी कीटों के प्रवेश और प्रसार को रोकता है और कृषि जिंसों में सुरक्षित वैश्विक व्यापार की सुविधा प्रदान करता है।", mr: "भारतात विदेशी कीटकांचा प्रवेश आणि प्रसार रोखते आणि कृषी मालाच्या सुरक्षित जागतिक व्यापारास सुलभ करते." }, link: "https://ppqs.gov.in/" },
    { id: 6, title: { en: "Indian Council of Agricultural Research (ICAR)", hi: "भारतीय कृषि अनुसंधान परिषद (आईसीएआर)", mr: "भारतीय कृषी संशोधन परिषद (आयसीएआर)" }, description: { en: "The apex body for coordinating, guiding, and managing research and education in agriculture including horticulture, fisheries, and animal sciences.", hi: "बागवानी, मत्स्य पालन और पशु विज्ञान सहित कृषि में अनुसंधान और शिक्षा के समन्वय, मार्गदर्शन और प्रबंधन के लिए शीर्ष निकाय।", mr: "बागायती, मत्स्यपालन आणि पशु विज्ञान यासह कृषीमधील संशोधन आणि शिक्षणाचे समन्वय, मार्गदर्शन आणि व्यवस्थापन करणारी सर्वोच्च संस्था." }, link: "https://icar.org.in/" },
    { id: 7, title: { en: "Krishi Vigyan Kendra (KVK)", hi: "कृषि विज्ञान केंद्र (केवीके)", mr: "कृषी विज्ञान केंद्र (केव्हीके)" }, description: { en: "District-level farm science centers that act as a bridge between research institutions and farmers, providing technology assessment and demonstration.", hi: "जिला स्तरीय कृषि विज्ञान केंद्र जो अनुसंधान संस्थानों और किसानों के बीच एक सेतु के रूप में कार्य करते हैं, प्रौद्योगिकी मूल्यांकन और प्रदर्शन प्रदान करते हैं।", mr: "जिल्हास्तरीय कृषी विज्ञान केंद्रे जी संशोधन संस्था आणि शेतकरी यांच्यात एक पूल म्हणून काम करतात, तंत्रज्ञान मूल्यांकन आणि प्रात्यक्षिक प्रदान करतात." }, link: "https://kvk.icar.gov.in/" },
    { id: 8, title: { en: "National Informatics Centre - Agriculture Division", hi: "राष्ट्रीय सूचना विज्ञान केंद्र - कृषि प्रभाग", mr: "राष्ट्रीय सूचना विज्ञान केंद्र - कृषी विभाग" }, description: { en: "Provides ICT infrastructure and e-governance solutions to the agricultural sector to enhance efficiency and transparency.", hi: "दक्षता और पारदर्शिता बढ़ाने के लिए कृषि क्षेत्र को आईसीटी बुनियादी ढांचा और ई-गवर्नेंस समाधान प्रदान करता है।", mr: "कार्यक्षमता आणि पारदर्शकता वाढवण्यासाठी कृषी क्षेत्राला आयसीटी पायाभूत सुविधा आणि ई-गव्हर्नन्स सोल्यूशन्स प्रदान करते." }, link: "https://agriculture.nic.in/" },
    { id: 9, title: { en: "Ministry of Agriculture & Farmers Welfare", hi: "कृषि एवं किसान कल्याण मंत्रालय", mr: "कृषी आणि शेतकरी कल्याण मंत्रालय" }, description: { en: "The apex government body responsible for rules, regulations, and laws related to agriculture in India.", hi: "भारत में कृषि से संबंधित नियमों, विनियमों और कानूनों के लिए जिम्मेदार शीर्ष सरकारी निकाय।", mr: "भारतातील शेतीशी संबंधित नियम, कायदे आणि कायद्यांसाठी जबाबदार असलेली सर्वोच्च सरकारी संस्था." }, link: "https://agriculture.gov.in/" },
    { id: 10, title: { en: "eNAM (National Agriculture Market)", hi: "ई-नाम (राष्ट्रीय कृषि बाजार)", mr: "ई-नाम (राष्ट्रीय कृषी बाजार)" }, description: { en: "A pan-India electronic trading portal that creates a unified national market for agricultural commodities.", hi: "एक अखिल भारतीय इलेक्ट्रॉनिक ट्रेडिंग पोर्टल जो कृषि जिंसों के लिए एक एकीकृत राष्ट्रीय बाजार बनाता है।", mr: "एक अखिल भारतीय इलेक्ट्रॉनिक ट्रेडिंग पोर्टल जे कृषी मालासाठी एक एकीकृत राष्ट्रीय बाजारपेठ तयार करते." }, link: "https://enam.gov.in/" },
    { id: 11, title: { en: "Soil Health Card Portal", hi: "मृदा स्वास्थ्य कार्ड पोर्टल", mr: "मृदा आरोग्य कार्ड पोर्टल" }, description: { en: "Provides farmers with soil nutrient status and recommendations on appropriate dosage of nutrients for improving soil health.", hi: "किसानों को मिट्टी की पोषक स्थिति और मिट्टी के स्वास्थ्य में सुधार के लिए पोषक तत्वों की उचित खुराक पर सिफारिशें प्रदान करता है।", mr: "शेतकऱ्यांना मातीची पोषक स्थिती आणि मातीचे आरोग्य सुधारण्यासाठी पोषक तत्वांच्या योग्य मात्रेबद्दल शिफारसी प्रदान करते." }, link: "https://soilhealth.dac.gov.in/" },
    { id: 12, title: { en: "Agri Market Information System (Agmarknet)", hi: "कृषि बाजार सूचना प्रणाली (एगमार्कनेट)", mr: "कृषी बाजार माहिती प्रणाली (एगमार्कनेट)" }, description: { en: "A government portal providing information on wholesale market prices, arrivals, and trends for agricultural commodities.", hi: "कृषि जिंसों के लिए थोक बाजार की कीमतों, आगमन और प्रवृत्तियों पर जानकारी प्रदान करने वाला एक सरकारी पोर्टल।", mr: "कृषी मालाच्या घाऊक बाजारातील किमती, आवक आणि ट्रेंड यावर माहिती देणारे सरकारी पोर्टल." }, link: "https://agmarknet.gov.in/" }
];

const dummyProducts = [
  // Vegetables
  { id: 1, name: "Organic Potatoes", imageUrl: "https://placehold.co/150x100/F0E68C/000000?text=Potatoes" },
  { id: 2, name: "Organic Onions", imageUrl: "https://placehold.co/150x100/DDA0DD/000000?text=Onions" },
  { id: 3, name: "Organic Tomatoes", imageUrl: "https://placehold.co/150x100/FF6347/000000?text=Tomatoes" },
  { id: 4, name: "Organic Spinach", imageUrl: "https://placehold.co/150x100/3CB371/000000?text=Spinach" },
  { id: 5, name: "Organic Cauliflower", imageUrl: "https://placehold.co/150x100/F5FFFA/000000?text=Cauliflower" },
  { id: 6, name: "Organic Brinjal", imageUrl: "https://placehold.co/150x100/4B0082/FFFFFF?text=Brinjal" },
  { id: 7, name: "Organic Ladyfinger", imageUrl: "https://placehold.co/150x100/9ACD32/000000?text=Okra" },
  { id: 8, name: "Organic Carrots", imageUrl: "https://placehold.co/150x100/FFA500/000000?text=Carrots" },
  // Fruits
  { id: 9, name: "Organic Apples", imageUrl: "https://placehold.co/150x100/FF4500/000000?text=Apples" },
  { id: 10, name: "Organic Bananas", imageUrl: "https://placehold.co/150x100/FFFF00/000000?text=Bananas" },
  { id: 11, name: "Organic Mangoes", imageUrl: "https://placehold.co/150x100/FFD700/000000?text=Mangoes" },
  { id: 12, name: "Organic Pomegranate", imageUrl: "https://placehold.co/150x100/DC143C/FFFFFF?text=Pomegranate" },
  // Grains & Pulses
  { id: 13, name: "Organic Basmati Rice", imageUrl: "https://placehold.co/150x100/A0E7A0/000000?text=Basmati+Rice" },
  { id: 14, name: "Organic Wheat Flour", imageUrl: "https://placehold.co/150x100/E7A0A0/000000?text=Wheat+Flour" },
  { id: 15, name: "Organic Moong Dal", imageUrl: "https://placehold.co/150x100/A0A0E7/000000?text=Moong+Dal" },
  { id: 16, name: "Organic Toor Dal", imageUrl: "https://placehold.co/150x100/F0E68C/000000?text=Toor+Dal" },
  { id: 17, name: "Organic Chana Dal", imageUrl: "https://placehold.co/150x100/DAA520/000000?text=Chana+Dal" },
  { id: 18, name: "Organic Millets", imageUrl: "https://placehold.co/150x100/BDB76B/000000?text=Millets" },
  // Spices & Others
  { id: 19, name: "Organic Turmeric Powder", imageUrl: "https://placehold.co/150x100/E7E7A0/000000?text=Turmeric" },
  { id: 20, name: "Organic Ghee", imageUrl: "https://placehold.co/150x100/FFFACD/000000?text=Ghee" },
  { id: 21, name: "Organic Jaggery", imageUrl: "https://placehold.co/150x100/8B4513/FFFFFF?text=Jaggery" },
  { id: 22, name: "Organic Honey", imageUrl: "https://placehold.co/150x100/FFA500/000000?text=Honey" },
];

const dummyStudyMaterials = [
  {
    id: 1,
    type: "beginner",
    title: { en: "Basics of Composting", hi: "खाद बनाने की मूल बातें", mr: "कंपोस्टिंगची मूलभूत माहिती" },
    link: "https://www.youtube.com/embed/is5_X9q3w58" // Example YouTube embed
  },
  {
    id: 2,
    type: "advanced",
    title: { en: "Soil Microbiology in Organic Farming", hi: "जैविक खेती में मृदा सूक्ष्म जीव विज्ञान", mr: "सेंद्रिय शेतीत मातीचे सूक्ष्मजीवशास्त्र" },
    link: "https://www.youtube.com/embed/5y0iP-hM0sE"
  },
  {
    id: 3,
    type: "university",
    title: { en: "NPTEL Course: Organic Farming for Sustainable Production", hi: "एनपीटीईएल कोर्स: सतत उत्पादन के लिए जैविक खेती", mr: "एनपीटीईएल कोर्स: शाश्वत उत्पादनासाठी सेंद्रिय शेती" },
    link: "https://elearn.nptel.ac.in/shop/nptel/organic-farming-for-sustainable-agricultural-production/"
  },
  {
    id: 4,
    type: "gov_pub",
    title: { en: "Guide to PGS-India Certification", hi: "पीजीएस-इंडिया प्रमाणीकरण के लिए गाइड", mr: "पीजीएस-इंडिया प्रमाणनासाठी मार्गदर्शक" },
    link: "https://pgsindia-ncof.gov.in/Pdf/Manual/PGS-India%20Operational%20Manual%20(English).pdf"
  }
];

const dummyAwards = [
  {
    id: 1,
    name: { en: "Jaivik India Awards", hi: "जैविक भारत पुरस्कार", mr: "जैविक भारत पुरस्कार" },
    organizer: { en: "ICCOA", hi: "आईसीओए", mr: "आयसीसीओए" },
    year: 2022,
    winners: { en: "Rahul Kumar (MP), Hanamanth Halaki (Karnataka), Yogita Gajanan Dhurve (Maharashtra)", hi: "राहुल कुमार (म.प्र.), हनुमंत हलाकी (कर्नाटक), योगिता गजानन धुर्वे (महाराष्ट्र)", mr: "राहुल कुमार (म.प्र.), हनुमंत हलाकी (कर्नाटक), योगिता गजानन धुर्वे (महाराष्ट्र)" },
    location: { en: "Agra, India", hi: "आगरा, भारत", mr: "आग्रा, भारत" }
  },
  {
    id: 2,
    name: { en: "EU Organic Awards", hi: "ईयू जैविक पुरस्कार", mr: "युरोपियन युनियन सेंद्रिय पुरस्कार" },
    organizer: { en: "European Commission, IFOAM Organics Europe", hi: "यूरोपीय आयोग, आईफोम ऑर्गेनिक्स यूरोप", mr: "युरोपियन कमिशन, आयफोम ऑरगॅनिक्स युरोप" },
    year: 2024,
    winners: { en: "Reinhilde Frech-Emmelmann (Austria), Benny Schöpf (Germany)", hi: "रेनहिल्ड फ्रेच-एम्मेलमैन (ऑस्ट्रिया), बेनी शोफ (जर्मनी)", mr: "रेनहिल्ड फ्रेच-एम्मेलमन (ऑस्ट्रिया), बेनी शोफ (जर्मनी)" },
    location: { en: "Brussels, Belgium", hi: "ब्रसेल्स, बेल्जियम", mr: "ब्रसेल्स, बेल्जियम" }
  },
  {
    id: 3,
    name: { en: "Organic Farming Innovation Award (OFIA)", hi: "जैविक खेती नवाचार पुरस्कार (ओएफआईए)", mr: "सेंद्रिय शेती नवोपक्रम पुरस्कार (ओएफआयए)" },
    organizer: { en: "IFOAM - Organics International, RDA South Korea", hi: "आईफोम - ऑर्गेनिक्स इंटरनेशनल, आरडीए दक्षिण कोरिया", mr: "आयफोम - ऑरगॅनिक्स इंटरनॅशनल, आरडीए दक्षिण कोरिया" },
    year: 2021,
    winners: { en: "Dr. Shaikh Tanveer Hossain (Bangladesh), Mike Hands (UK)", hi: "डॉ. शेख तनवीर हुसैन (बांग्लादेश), माइक हैंड्स (यूके)", mr: "डॉ. शेख तनवीर हुसेन (बांगलादेश), माईक हँड्स (यूके)" },
    location: { en: "Various (Online/Conferences)", hi: "विभिन्न (ऑनलाइन/सम्मेलन)", mr: "विविध (ऑनलाइन/परिषदा)" }
  }
];

const dummyDemandData = {
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [77.2090, 28.6139] }, // Delhi
      "properties": { "name": "Delhi", "organic_fertilizer_demand_usd_mn": 25, "biopesticide_adoption_rate_percent": 18, "certified_organic_area_hectares": 5000 }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [72.8777, 19.0760] }, // Mumbai
      "properties": { "name": "Mumbai", "organic_fertilizer_demand_usd_mn": 35, "biopesticide_adoption_rate_percent": 22, "certified_organic_area_hectares": 7000 }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [77.5946, 12.9716] }, // Bangalore
      "properties": { "name": "Bengaluru", "organic_fertilizer_demand_usd_mn": 30, "biopesticide_adoption_rate_percent": 20, "certified_organic_area_hectares": 6500 }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [78.4867, 17.3850] }, // Hyderabad
      "properties": { "name": "Hyderabad", "organic_fertilizer_demand_usd_mn": 28, "biopesticide_adoption_rate_percent": 19, "certified_organic_area_hectares": 6000 }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [80.9462, 26.8467] }, // Lucknow
      "properties": { "name": "Lucknow", "organic_fertilizer_demand_usd_mn": 15, "biopesticide_adoption_rate_percent": 10, "certified_organic_area_hectares": 3000 }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [75.8577, 22.7196] }, // Indore
      "properties": { "name": "Indore", "organic_fertilizer_demand_usd_mn": 18, "biopesticide_adoption_rate_percent": 15, "certified_organic_area_hectares": 4500 }
    },
    {
      "type": "Feature",
      "geometry": { "type": "Point", "coordinates": [74.7764, 15.3647] }, // Hubli
      "properties": { "name": "Hubli", "organic_fertilizer_demand_usd_mn": 10, "biopesticide_adoption_rate_percent": 8, "certified_organic_area_hectares": 2000 }
    }
  ]
};

const dummyGovCertifications = [
    { id: 1, title: "Thirty-days Certificate Course on Organic Farming (NCOF)", provider: "National Centre for Organic and Natural Farming", url: "https://ncof.dacnet.nic.in/training_30days.aspx" },
    { id: 2, title: "Certificate Course on Post-Harvest Handling and Storage of Food Commodities", provider: "ICAR-CIPHET", url: "https://ciphet.icar.gov.in/" },
    { id: 3, title: "Certificate Courses Online Registration", provider: "Kerala Agricultural University (KAU)", url: "https://www.kau.in/academics/certificate-courses" },
    { id: 4, title: "New Generation Certificate Courses", provider: "Kerala Agricultural University (KAU)", url: "https://www.kau.in/academics/new-generation-certificate-courses" },
    { id: 5, title: "Certificate in Organic Farming", provider: "IGNOU", url: "https://www.ignou.ac.in/schools/programme/COF" }
];

const dummyPrivateCertifications = [
    { id: 1, title: "Organic Farming Business Course (IID)", provider: "IID Online Learning", url: "https://courses.iid.org.in/course/organic-farming" },
    { id: 2, title: "Organic Vegetable Cultivation Course (IID)", provider: "IID Online Learning", url: "https://courses.iid.org.in/course/organic-vegetable-cultivation-c" },
    { id: 3, title: "Organic Farming (SIILC, Pune)", provider: "SIILC", url: "https://www.siilc.edu.in/courses/courses/organic-farming/" },
    { id: 4, title: "SIILC Agriculture Courses page", provider: "SIILC", url: "https://www.siilc.edu.in/courses/agriculture/" },
    { id: 5, title: "Certificate in Organic Grower (IISDT)", provider: "IISDT", url: "https://iisdt.in/product/certificate-in-organic-grower/" },
    { id: 6, title: "Certificate in Organic Agriculture (IISDT)", provider: "IISDT", url: "https://iisdt.in/product/certificate-in-organic-agriculture/" }
];

const dummyCourses = [
  { id: 1, title: "agMOOCs", provider: "agMOOCs", url: "https://agmoocs.in/" },
  { id: 2, title: "Certificate in Organic Farming", provider: "IGNOU", url: "https://www.ignou.ac.in/schools/programme/COF" },
  { id: 3, title: "Introduction to Farm Machinery and Implement", provider: "SWAYAM", url: "https://onlinecourses.swayam2.ac.in/nou25_ag09/preview" },
  { id: 4, title: "Organic Farming Practices and Certification", provider: "SWAYAM", url: "https://www.getyoureducation.net/course/organic-farming-practices-and-certification" },
  { id: 5, title: "Post Graduate Certificate in Agriculture Policy", provider: "IGNOU", url: "https://www.ignou.ac.in/schools/programme/PGCAPOL" },
  { id: 6, title: "PG Diploma in Agribusiness", provider: "IGNOU", url: "https://www.ignou.ac.in/schools/programme/PGDAB" },
  { id: 7, title: "Certificate in Gender, Agriculture and Sustainable Development", provider: "IGNOU", url: "https://www.ignou.ac.in/schools/programme/CGAS" },
  { id: 8, title: "Diploma in Agricultural Cost Management", provider: "IGNOU", url: "https://www.ignou.ac.in/schools/programme/DACM" },
];

const dummyWeatherData = {
  current: {
    location: "Pimpri-Chinchwad, Maharashtra",
    temp_c: 28,
    condition: { en: "Partly Cloudy", hi: "आंशिक रूप से बादल छाए हुए हैं", mr: "अंशतः ढगाळ" },
    humidity: 75,
    wind_kph: 10,
    icon: "cloudy"
  },
  forecast: [
    { date: "Sep 19", day: { en: "Fri", hi: "शुक्र", mr: "शुक्र" }, maxtemp_c: 32, mintemp_c: 24, condition: { en: "Partly Cloudy", hi: "आंशिक रूप से बादल", mr: "अंशतः ढगाळ" }, icon: "cloudy" },
    { date: "Sep 20", day: { en: "Sat", hi: "शनि", mr: "शनि" }, maxtemp_c: 31, mintemp_c: 25, condition: { en: "Sunny Intervals", hi: "धूप के साथ अंतराल", mr: "अधूनमधून सूर्यप्रकाश" }, icon: "sun-cloud" },
    { date: "Sep 21", day: { en: "Sun", hi: "रवि", mr: "रवि" }, maxtemp_c: 33, mintemp_c: 25, condition: { en: "Sunny", hi: "धूप", mr: "सूर्यप्रकाश" }, icon: "sun" },
    { date: "Sep 22", day: { en: "Mon", hi: "सोम", mr: "सोम" }, maxtemp_c: 30, mintemp_c: 24, condition: { en: "Light Rain", hi: "हल्की बारिश", mr: "हलका पाऊस" }, icon: "rain" },
    { date: "Sep 23", day: { en: "Tue", hi: "मंगल", mr: "मंगळ" }, maxtemp_c: 31, mintemp_c: 24, condition: { en: "Partly Cloudy", hi: "आंशिक रूप से बादल", mr: "अंशतः ढगाळ" }, icon: "cloudy" },
  ]
};


// --- Components ---

const Header = ({ onLanguageChange, currentLanguage, isLoggedIn, onLogout }) => {
  const t = translations[currentLanguage];

  return (
    <header className="bg-green-700 text-white p-4 shadow-md rounded-b-lg">
      <nav className="container mx-auto flex flex-col md:flex-row justify-between items-center">
        <div className="text-2xl font-bold mb-2 md:mb-0">
          <a href="/" className="hover:text-green-200 transition-colors">OrganicFarmHub</a>
        </div>
        <ul className="flex flex-wrap justify-center gap-x-4 gap-y-2 md:gap-x-6 text-lg mb-2 md:mb-0">
          <li><a href="/" className="hover:text-green-200 transition-colors">{t.home}</a></li>
          <li><a href="#schemes" className="hover:text-green-200 transition-colors">{t.schemes}</a></li>
          <li><a href="#products" className="hover:text-green-200 transition-colors">{t.products}</a></li>
          <li><a href="#learning" className="hover:text-green-200 transition-colors">{t.learning}</a></li>
          <li><a href="#awards" className="hover:text-green-200 transition-colors">{t.awards}</a></li>
          <li><a href="#demand" className="hover:text-green-200 transition-colors">{t.demand}</a></li>
          <li><a href="#certification" className="hover:text-green-200 transition-colors">{t.certification}</a></li>
          <li><a href="#scanner" className="hover:text-green-200 transition-colors">{t.scanner}</a></li>
          <li><a href="#weather" className="hover:text-green-200 transition-colors">{t.weather}</a></li>
          <li><a href="#contact" className="hover:text-green-200 transition-colors">{t.contactUs}</a></li>
        </ul>
        <div className="flex items-center space-x-4">
          {isLoggedIn ? (
            <>
              <a href="#dashboard" className="bg-green-600 hover:bg-green-500 text-white px-4 py-2 rounded-full shadow-md transition-colors">{t.viewProfile}</a>
              <button onClick={onLogout} className="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-full shadow-md transition-colors">{t.logout}</button>
            </>
          ) : (
            <>
              <a href="#login" className="bg-green-600 hover:bg-green-500 text-white px-4 py-2 rounded-full shadow-md transition-colors">{t.login}</a>
              <a href="#register" className="bg-green-600 hover:bg-green-500 text-white px-4 py-2 rounded-full shadow-md transition-colors">{t.register}</a>
            </>
          )}
          <select
            onChange={(e) => onLanguageChange(e.target.value)}
            value={currentLanguage}
            className="bg-green-600 text-white p-2 rounded-md cursor-pointer"
          >
            <option value="en">English</option>
            <option value="hi">हिन्दी</option>
            <option value="mr">मराठी</option>
          </select>
        </div>
      </nav>
    </header>
  );
};

const Footer = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  return (
    <footer className="bg-gray-800 text-white p-6 mt-10 rounded-t-lg">
      <div className="container mx-auto text-center">
        <h3 className="text-xl font-semibold mb-3">{t.contactUs}</h3>
        <p className="mb-1">{t.contactInfo}</p>
        <p className="mb-1">Email: <a href={`mailto:${t.emailAddress}`} className="text-green-400 hover:underline">{t.emailAddress}</a></p>
        <p className="mb-4">Phone: <a href={`tel:${t.phoneNumber}`} className="text-green-400 hover:underline">{t.phoneNumber}</a></p>
        <div className="flex justify-center space-x-4 mb-4">
          <a href="#" className="text-green-400 hover:text-green-200"><i className="fab fa-facebook-f"></i></a>
          <a href="#" className="text-green-400 hover:text-green-200"><i className="fab fa-twitter"></i></a>
          <a href="#" className="text-green-400 hover:text-green-200"><i className="fab fa-instagram"></i></a>
          <a href="#" className="text-green-400 hover:text-green-200"><i className="fab fa-linkedin-in"></i></a>
          <a href="#" className="text-green-400 hover:text-green-200"><i className="fab fa-youtube"></i></a>
        </div>
        <p className="text-sm">{t.footerText}</p>
      </div>
    </footer>
  );
};

const HomePage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  return (
    <section className="container mx-auto p-6 text-center">
      <div className="bg-green-100 p-8 rounded-lg shadow-lg mb-8">
        <h1 className="text-5xl font-extrabold text-green-800 mb-4 animate-fade-in-down">{t.welcome}</h1>
        <p className="text-xl text-gray-700 mb-6 animate-fade-in-up">{t.tagline}</p>
        <img
          src="https://placehold.co/800x400/A0E7A0/000000?text=Organic+Farm+Image"
          alt="Organic Farm"
          className="w-full h-auto rounded-lg shadow-md mx-auto max-w-3xl"
          onError={(e) => { e.target.onerror = null; e.target.src = 'https://placehold.co/800x400/CCCCCC/000000?text=Image+Not+Available'; }}
        />
      </div>

      <div className="grid md:grid-cols-2 gap-8 text-left">
        <div className="bg-white p-6 rounded-lg shadow-md">
          <h2 className="text-3xl font-bold text-green-700 mb-4">{t.aboutUs}</h2>
          <p className="text-gray-700 leading-relaxed">{t.aboutUsContent}</p>
        </div>
        <div className="bg-white p-6 rounded-lg shadow-md">
          <h2 className="text-3xl font-bold text-green-700 mb-4">{t.learningResources}</h2>
          <p className="text-gray-700 leading-relaxed">
            Explore our extensive library of articles, guides, and videos to deepen your knowledge of organic farming. From beginner basics to advanced techniques, we have resources for every level.
          </p>
          <a href="#learning" className="text-green-600 hover:underline mt-4 inline-block font-semibold">Learn More &rarr;</a>
        </div>
      </div>
    </section>
  );
};

const SchemesPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  return (
    <section id="schemes" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.schemes}</h2>

      <div className="mb-10">
        <h3 className="text-3xl font-semibold text-green-700 mb-6 border-b-2 border-green-500 pb-2">{t.govSchemes} for Organic Farming</h3>
        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          {dummySchemes.map(scheme => (
            <div key={scheme.id} className="bg-white p-6 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
              <h4 className="text-xl font-bold text-gray-800 mb-2">{scheme.title[currentLanguage]}</h4>
              <p className="text-gray-600 text-sm mb-3">{scheme.description[currentLanguage]}</p>
              <p className="text-gray-700 mb-1"><strong>{t.schemeEligibility}:</strong> {scheme.eligibility[currentLanguage]}</p>
              <p className="text-gray-700 mb-3"><strong>{t.schemeBenefits}:</strong> {scheme.benefits[currentLanguage]}</p>
              <a href={scheme.link} target="_blank" rel="noopener noreferrer" className="text-green-600 hover:underline font-semibold">{t.schemeLink} &rarr;</a>
            </div>
          ))}
        </div>
      </div>
      
      <div className="mb-10">
        <h3 className="text-3xl font-semibold text-green-700 mb-6 border-b-2 border-green-500 pb-2">{t.generalFarmerSchemes}</h3>
        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          {dummyGeneralFarmerSchemes.map(scheme => (
            <div key={scheme.id} className="bg-white p-6 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
              <h4 className="text-xl font-bold text-gray-800 mb-2">{scheme.title[currentLanguage]}</h4>
              <p className="text-gray-600 text-sm mb-3">{scheme.description[currentLanguage]}</p>
              <p className="text-gray-700 mb-1"><strong>{t.schemeEligibility}:</strong> {scheme.eligibility[currentLanguage]}</p>
              <p className="text-gray-700 mb-3"><strong>{t.schemeBenefits}:</strong> {scheme.benefits[currentLanguage]}</p>
              <a href={scheme.link} target="_blank" rel="noopener noreferrer" className="text-green-600 hover:underline font-semibold">{t.schemeLink} &rarr;</a>
            </div>
          ))}
        </div>
      </div>

      <div className="mb-10">
        <h3 className="text-3xl font-semibold text-green-700 mb-6 border-b-2 border-green-500 pb-2">{t.autonomousBodies}</h3>
        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          {dummySupportBodies.map(body => (
            <div key={body.id} className="bg-white p-6 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
              <h4 className="text-xl font-bold text-gray-800 mb-2">{body.title[currentLanguage]}</h4>
              <p className="text-gray-600 text-sm mb-3">{body.description[currentLanguage]}</p>
              <a href={body.link} target="_blank" rel="noopener noreferrer" className="text-green-600 hover:underline font-semibold">{t.schemeLink} &rarr;</a>
            </div>
          ))}
        </div>
      </div>

      <div>
        <h3 className="text-3xl font-semibold text-green-700 mb-6 border-b-2 border-green-500 pb-2">{t.privateSchemes}</h3>
        <p className="text-gray-700">
          (Information on private initiatives and NGOs promoting organic farming would be listed here, similar to government schemes.)
          <br/>
          Example: Organic India Foundation, various local NGOs providing training and support.
        </p>
      </div>
    </section>
  );
};

const ProductsPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [searchTerm, setSearchTerm] = useState('');
  const [selectedProduct, setSelectedProduct] = useState(null);
  const [prices, setPrices] = useState(null);
  const [loadingPrices, setLoadingPrices] = useState(false);
  const [priceError, setPriceError] = useState(null);

  const handleSearch = (e) => {
    setSearchTerm(e.target.value);
  };

  const filteredProducts = dummyProducts.filter(product =>
    product.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  const compareProductPrices = async (productName) => {
    setSelectedProduct(productName);
    setLoadingPrices(true);
    setPriceError(null);
    setPrices(null); // Clear previous prices

    // Simulate API call to fetch prices from different platforms
    await new Promise(resolve => setTimeout(resolve, 1500)); // Simulate network delay

    const dummyFetchedPrices = {
      amazon: `₹${(Math.random() * 50 + 150).toFixed(2)}`,  // Base price
      flipkart: `₹${(Math.random() * 50 + 145).toFixed(2)}`, // Slightly competitive
      mesho: `₹${(Math.random() * 50 + 140).toFixed(2)}`,   // Often cheaper
      shopsy: `₹${(Math.random() * 50 + 142).toFixed(2)}`,   // Similar to Mesho
      zomato: `₹${(Math.random() * 50 + 180).toFixed(2)}`,  // Higher due to delivery
      swiggy: `₹${(Math.random() * 50 + 185).toFixed(2)}`,  // Similar to Zomato
      local_store: `₹${(Math.random() * 50 + 130).toFixed(2)}`, // Potentially cheapest
    };

    // Simulate potential error
    if (Math.random() < 0.1) { // 10% chance of error
      setPriceError(t.priceError);
    } else {
      setPrices(dummyFetchedPrices);
    }
    setLoadingPrices(false);
  };

  const getSortedPrices = (fetchedPrices) => {
    if (!fetchedPrices) return [];
    const entries = Object.entries(fetchedPrices).map(([platform, priceStr]) => {
      const priceValue = parseFloat(priceStr.replace(/[^0-9.]/g, ''));
      const platformUrls = {
        amazon: `https://www.amazon.in/s?k=${encodeURIComponent(selectedProduct)}`,
        flipkart: `https://www.flipkart.com/search?q=${encodeURIComponent(selectedProduct)}`,
        mesho: `https://www.meesho.com/search?q=${encodeURIComponent(selectedProduct)}`,
        shopsy: `https://www.shopsy.in/search?q=${encodeURIComponent(selectedProduct)}`,
        zomato: 'https://www.zomato.com/groceries',
        swiggy: 'https://www.swiggy.com/instamart',
        local_store: '#'
      };
      return { platform, priceStr, priceValue, url: platformUrls[platform] || '#' };
    });
    return entries.sort((a, b) => a.priceValue - b.priceValue);
  };

  const sortedPrices = getSortedPrices(prices);

  return (
    <section id="products" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-4 text-center">{t.productCatalog}</h2>

      {/* New Row for Links and Update Button */}
      <div className="flex justify-between items-center mb-6 px-1 md:px-4">
        {/* Official Sites Dropdown */}
        <div className="relative group">
          <button className="bg-gray-200 text-gray-800 font-semibold py-2 px-4 rounded-lg inline-flex items-center shadow-sm">
            <span>{t.officialSites}</span>
            <svg className="fill-current h-4 w-4 ml-2" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
          </button>
          <ul className="absolute hidden text-gray-700 pt-1 group-hover:block bg-white shadow-lg rounded-lg z-10 w-40">
            <li><a className="rounded-t hover:bg-gray-200 py-2 px-4 block whitespace-no-wrap" href="https://www.amazon.in" target="_blank" rel="noopener noreferrer">Amazon</a></li>
            <li><a className="hover:bg-gray-200 py-2 px-4 block whitespace-no-wrap" href="https://www.flipkart.com" target="_blank" rel="noopener noreferrer">Flipkart</a></li>
            <li><a className="hover:bg-gray-200 py-2 px-4 block whitespace-no-wrap" href="https://www.meesho.com" target="_blank" rel="noopener noreferrer">Meesho</a></li>
            <li><a className="hover:bg-gray-200 py-2 px-4 block whitespace-no-wrap" href="https://www.shopsy.in" target="_blank" rel="noopener noreferrer">Shopsy</a></li>
            <li><a className="hover:bg-gray-200 py-2 px-4 block whitespace-no-wrap" href="https://www.zomato.com/groceries" target="_blank" rel="noopener noreferrer">Zomato</a></li>
            <li><a className="rounded-b hover:bg-gray-200 py-2 px-4 block whitespace-no-wrap" href="https://www.swiggy.com/instamart" target="_blank" rel="noopener noreferrer">Swiggy Instamart</a></li>
          </ul>
        </div>

        {/* Update Prices Button */}
        <button
          onClick={() => compareProductPrices(selectedProduct)}
          disabled={!selectedProduct || loadingPrices}
          className="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg flex items-center transition-colors shadow-md disabled:bg-gray-400 disabled:cursor-not-allowed"
        >
          <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5 mr-2" viewBox="0 0 20 20" fill="currentColor">
            <path fillRule="evenodd" d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z" clipRule="evenodd" />
          </svg>
          {t.updatePrices}
        </button>
      </div>


      <div className="mb-8 text-center">
        <input
          type="text"
          placeholder={t.searchProduct}
          className="p-3 border border-gray-300 rounded-lg w-full max-w-md focus:outline-none focus:ring-2 focus:ring-green-500 shadow-sm"
          value={searchTerm}
          onChange={handleSearch}
        />
      </div>

      <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
        {filteredProducts.length > 0 ? (
          filteredProducts.map(product => (
            <div key={product.id} className="bg-white p-6 rounded-lg shadow-md border border-green-200 text-center hover:shadow-lg transition-shadow">
              <img
                src={product.imageUrl}
                alt={product.name}
                className="w-full h-32 object-cover rounded-md mb-4 mx-auto"
                onError={(e) => { e.target.onerror = null; e.target.src = 'https://placehold.co/150x100/CCCCCC/000000?text=Product+Image'; }}
              />
              <h3 className="text-xl font-bold text-gray-800 mb-3">{product.name}</h3>
              <button
                onClick={() => compareProductPrices(product.name)}
                className="bg-green-600 hover:bg-green-700 text-white px-5 py-2 rounded-full shadow-md transition-colors"
              >
                {t.comparePrices}
              </button>
            </div>
          ))
        ) : (
          <p className="col-span-full text-center text-gray-600">No products found matching your search.</p>
        )}
      </div>

      {selectedProduct && (
        <div className="mt-10 bg-green-50 p-6 rounded-lg shadow-inner border border-green-300">
          <h3 className="text-2xl font-bold text-green-800 mb-4 text-center">
            {t.comparePrices} for {selectedProduct}
          </h3>
          {loadingPrices && <p className="text-center text-gray-600">{t.loadingPrices}</p>}
          {priceError && <p className="text-center text-red-500">{priceError}</p>}
          {prices && (
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
              {sortedPrices.map((item, index) => (
                <div
                  key={item.platform}
                  className={`p-4 rounded-lg shadow-sm ${index === 0 ? 'bg-yellow-100 border-yellow-400' : 'bg-white border-gray-200'} border`}
                >
                  <p className="text-lg font-semibold capitalize">
                    {item.platform.replace('_', ' ')}: <span className="text-green-700">{item.priceStr}</span>
                    {index === 0 && <span className="ml-2 px-2 py-1 bg-yellow-500 text-white text-xs rounded-full">{t.bestPrice}</span>}
                  </p>
                  <a href={item.url} target="_blank" rel="noopener noreferrer" className="text-blue-500 hover:underline text-sm">
                    {item.platform === 'local_store' ? 'Find local options' : `View on ${item.platform.charAt(0).toUpperCase() + item.platform.slice(1)}`}
                  </a>
                </div>
              ))}
            </div>
          )}
        </div>
      )}
    </section>
  );
};

const LearningPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [activeTab, setActiveTab] = useState('studyMaterials');

  const filteredMaterials = (type) => dummyStudyMaterials.filter(material => material.type === type);

  return (
    <section id="learning" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.learningResources}</h2>

      <div className="flex justify-center mb-8">
        <button
          className={`px-6 py-3 rounded-l-lg ${activeTab === 'studyMaterials' ? 'bg-green-600 text-white shadow-md' : 'bg-gray-200 text-gray-700 hover:bg-gray-300'} transition-colors`}
          onClick={() => setActiveTab('studyMaterials')}
        >
          {t.studyMaterials}
        </button>
        <button
          className={`px-6 py-3 rounded-r-lg ${activeTab === 'youtubeVideos' ? 'bg-green-600 text-white shadow-md' : 'bg-gray-200 text-gray-700 hover:bg-gray-300'} transition-colors`}
          onClick={() => setActiveTab('youtubeVideos')}
        >
          {t.youtubeVideos}
        </button>
      </div>

      {activeTab === 'studyMaterials' && (
        <div className="grid gap-8">
          <h3 className="text-3xl font-semibold text-green-700 mb-4 border-b-2 border-green-500 pb-2">{t.studyMaterials}</h3>

          <div className="mb-6">
            <h4 className="text-2xl font-bold text-gray-800 mb-3">{t.beginnerGuides}</h4>
            <div className="grid md:grid-cols-2 gap-4">
              {filteredMaterials('beginner').map(material => (
                <div key={material.id} className="bg-white p-5 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
                  <h5 className="text-xl font-semibold text-gray-800 mb-2">{material.title[currentLanguage]}</h5>
                  <a href={material.link} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline">View Guide &rarr;</a>
                </div>
              ))}
            </div>
          </div>

          <div className="mb-6">
            <h4 className="text-2xl font-bold text-gray-800 mb-3">{t.advancedTopics}</h4>
            <div className="grid md:grid-cols-2 gap-4">
              {filteredMaterials('advanced').map(material => (
                <div key={material.id} className="bg-white p-5 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
                  <h5 className="text-xl font-semibold text-gray-800 mb-2">{material.title[currentLanguage]}</h5>
                  <a href={material.link} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline">Read More &rarr;</a>
                </div>
              ))}
            </div>
          </div>

          <div className="mb-6">
            <h4 className="text-2xl font-bold text-gray-800 mb-3">{t.universityCourses}</h4>
            <div className="grid md:grid-cols-2 gap-4">
              {filteredMaterials('university').map(material => (
                <div key={material.id} className="bg-white p-5 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
                  <h5 className="text-xl font-semibold text-gray-800 mb-2">{material.title[currentLanguage]}</h5>
                  <a href={material.link} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline">Go to Course &rarr;</a>
                </div>
              ))}
            </div>
          </div>

          <div>
            <h4 className="text-2xl font-bold text-gray-800 mb-3">{t.govPublications}</h4>
            <div className="grid md:grid-cols-2 gap-4">
              {filteredMaterials('gov_pub').map(material => (
                <div key={material.id} className="bg-white p-5 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
                  <h5 className="text-xl font-semibold text-gray-800 mb-2">{material.title[currentLanguage]}</h5>
                  <a href={material.link} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline">View Document &rarr;</a>
                </div>
              ))}
            </div>
          </div>
        </div>
      )}

      {activeTab === 'youtubeVideos' && (
        <div>
          <div className="flex flex-wrap justify-between items-center mb-6 border-b-2 border-green-500 pb-2 gap-4">
            <h3 className="text-3xl font-semibold text-green-700">{t.youtubeVideos}</h3>
            <a
              href="https://www.youtube.com"
              target="_blank"
              rel="noopener noreferrer"
              className="bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg flex items-center transition-colors shadow-md"
            >
              <svg className="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"></path></svg>
              {t.visitYouTube}
            </a>
          </div>
          <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
            {dummyStudyMaterials.filter(m => m.link.includes('youtube.com/embed')).map(video => (
              <div key={video.id} className="bg-white rounded-lg shadow-md overflow-hidden border border-green-200">
                <div className="relative" style={{ paddingBottom: '56.25%', height: 0 }}>
                  <iframe
                    className="absolute top-0 left-0 w-full h-full"
                    src={video.link}
                    title={video.title[currentLanguage]}
                    frameBorder="0"
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                    allowFullScreen
                  ></iframe>
                </div>
                <div className="p-4">
                  <h4 className="text-xl font-semibold text-gray-800">{video.title[currentLanguage]}</h4>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}
    </section>
  );
};

const AwardsPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [activeTab, setActiveTab] = useState('national');

  const filteredAwards = (type) => {
    if (type === 'national') {
      return dummyAwards.filter(award => award.name.en.includes('Jaivik India Awards'));
    } else if (type === 'international') {
      return dummyAwards.filter(award => !award.name.en.includes('Jaivik India Awards'));
    }
    return [];
  };

  return (
    <section id="awards" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.awardsRecognition}</h2>

      <div className="flex justify-center mb-8">
        <button
          className={`px-6 py-3 rounded-l-lg ${activeTab === 'national' ? 'bg-green-600 text-white shadow-md' : 'bg-gray-200 text-gray-700 hover:bg-gray-300'} transition-colors`}
          onClick={() => setActiveTab('national')}
        >
          {t.nationalAwards}
        </button>
        <button
          className={`px-6 py-3 rounded-r-lg ${activeTab === 'international' ? 'bg-green-600 text-white shadow-md' : 'bg-gray-200 text-gray-700 hover:bg-gray-300'} transition-colors`}
          onClick={() => setActiveTab('international')}
        >
          {t.internationalAwards}
        </button>
      </div>

      <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        {filteredAwards(activeTab).map(award => (
          <div key={award.id} className="bg-white p-6 rounded-lg shadow-md border border-green-200 hover:shadow-lg transition-shadow">
            <h3 className="text-xl font-bold text-gray-800 mb-2">{award.name[currentLanguage]}</h3>
            <p className="text-gray-600 mb-1"><strong>{t.awardOrg}:</strong> {award.organizer[currentLanguage]}</p>
            <p className="text-gray-600 mb-1"><strong>{t.awardYear}:</strong> {award.year}</p>
            <p className="text-gray-700 mb-1"><strong>{t.awardWinners}:</strong> {award.winners[currentLanguage]}</p>
            <p className="text-gray-700"><strong>{t.location}:</strong> {award.location[currentLanguage]}</p>
          </div>
        ))}
      </div>
    </section>
  );
};

const MarketDemandPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [selectedState, setSelectedState] = useState('');
  const [selectedDistrict, setSelectedDistrict] = useState('');
  const [districts, setDistricts] = useState([]);
  const [searchTerm, setSearchTerm] = useState('');
  const [productsWithPrices, setProductsWithPrices] = useState([]);
  const [loading, setLoading] = useState(false);

  const handleStateChange = (e) => {
    const state = e.target.value;
    setSelectedState(state);
    setSelectedDistrict('');
    setProductsWithPrices([]);
    setDistricts(state ? indiaStates[state] : []);
  };

  const fetchPrices = async () => {
    if (!selectedState || !selectedDistrict) return;

    setLoading(true);
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500));

    const pricedProducts = farmProducts.map(product => {
        let basePrice;
        switch (product.category) {
            case 'Fruits': basePrice = 3000; break;
            case 'Vegetables': basePrice = 2000; break;
            case 'Spices & Condiments': basePrice = 8000; break;
            case 'Cereals / Grains': basePrice = 2500; break;
            case 'Pulses / Legumes': basePrice = 6000; break;
            case 'Oilseeds': basePrice = 5500; break;
            default: basePrice = 4000;
        }
        const price = basePrice + Math.floor(Math.random() * 2000) - 1000; // Add some variance
        return { ...product, price: `₹${price.toLocaleString('en-IN')}` };
    });

    setProductsWithPrices(pricedProducts);
    setLoading(false);
  };
  
  useEffect(() => {
    if (selectedDistrict) {
        fetchPrices();
    }
  }, [selectedDistrict]);

  const filteredProducts = productsWithPrices.filter(product =>
    product.name.toLowerCase().includes(searchTerm.toLowerCase())
  );
  
  const productCategories = [...new Set(filteredProducts.map(p => p.category))];


  return (
    <section id="demand" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.marketPrices}</h2>

      {/* Controls: Dropdowns, Search, and Update Button */}
      <div className="bg-white p-6 rounded-lg shadow-md border border-green-200 mb-8 sticky top-20 z-10">
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4 items-end">
          {/* State Dropdown */}
          <div>
            <label htmlFor="state-select" className="block text-sm font-medium text-gray-700">{t.selectState}</label>
            <select
              id="state-select"
              value={selectedState}
              onChange={handleStateChange}
              className="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-green-500 focus:border-green-500 sm:text-sm rounded-md"
            >
              <option value="">-- {t.selectState} --</option>
              {Object.keys(indiaStates).sort().map(state => (
                <option key={state} value={state}>{state}</option>
              ))}
            </select>
          </div>

          {/* District Dropdown */}
          <div>
            <label htmlFor="district-select" className="block text-sm font-medium text-gray-700">{t.selectDistrict}</label>
            <select
              id="district-select"
              value={selectedDistrict}
              onChange={(e) => setSelectedDistrict(e.target.value)}
              disabled={!selectedState}
              className="mt-1 block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-green-500 focus:border-green-500 sm:text-sm rounded-md disabled:bg-gray-100"
            >
              <option value="">-- {t.selectDistrict} --</option>
              {districts.sort().map(district => (
                <option key={district} value={district}>{district}</option>
              ))}
            </select>
          </div>

          {/* Search Input */}
          <div>
            <label htmlFor="product-search" className="block text-sm font-medium text-gray-700">{t.searchForProduct}</label>
            <input
              type="text"
              id="product-search"
              placeholder={t.searchForProduct}
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              disabled={!selectedDistrict}
              className="mt-1 block w-full shadow-sm sm:text-sm border-gray-300 rounded-md p-2 disabled:bg-gray-100"
            />
          </div>

          {/* Update Button */}
          <button
            onClick={fetchPrices}
            disabled={!selectedDistrict || loading}
            className="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg flex items-center justify-center transition-colors shadow-md disabled:bg-gray-400 disabled:cursor-not-allowed"
          >
            <svg xmlns="http://www.w3.org/2000/svg" className={`h-5 w-5 mr-2 ${loading ? 'animate-spin' : ''}`} viewBox="0 0 20 20" fill="currentColor">
                <path fillRule="evenodd" d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z" clipRule="evenodd" />
            </svg>
            {loading ? t.loading : t.updatePrices}
          </button>
        </div>
      </div>
      
      {/* Price Display Area */}
      <div className="mt-8">
        {!selectedDistrict ? (
            <p className="text-center text-gray-500 text-lg">{t.noPrices}</p>
        ) : loading ? (
             <p className="text-center text-gray-500 text-lg">{t.loading}</p>
        ) : (
            productCategories.map(category => (
                <div key={category} className="mb-8">
                    <h3 className="text-2xl font-semibold text-green-700 mb-4 border-b-2 border-green-300 pb-2">{category}</h3>
                    <div className="overflow-x-auto bg-white rounded-lg shadow">
                         <table className="min-w-full divide-y divide-gray-200">
                            <thead className="bg-gray-50">
                                <tr>
                                    <th scope="col" className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">{t.product}</th>
                                    <th scope="col" className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">{t.price}</th>
                                </tr>
                            </thead>
                            <tbody className="bg-white divide-y divide-gray-200">
                                {filteredProducts.filter(p => p.category === category).map((product, index) => (
                                    <tr key={index} className="hover:bg-gray-50">
                                        <td className="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">{product.name}</td>
                                        <td className="px-6 py-4 whitespace-nowrap text-sm text-gray-700 font-semibold">{product.price}</td>
                                    </tr>
                                ))}
                            </tbody>
                        </table>
                    </div>
                </div>
            ))
        )}
      </div>
    </section>
  );
};


const AIScannerPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [image, setImage] = useState(null);
  const [previewUrl, setPreviewUrl] = useState(null);
  const [scanning, setScanning] = useState(false);
  const [result, setResult] = useState(null);
  const [error, setError] = useState(null);

  const handleImageChange = (e) => {
    const file = e.target.files[0];
    if (file) {
      setImage(file);
      setPreviewUrl(URL.createObjectURL(file));
      setResult(null);
      setError(null);
    } else {
      setImage(null);
      setPreviewUrl(null);
      setResult(null);
      setError(null);
    }
  };

  const handleScan = async () => {
    if (!image) {
      setError(t.noImage);
      return;
    }

    setScanning(true);
    setResult(null);
    setError(null);

    // Simulate AI processing
    await new Promise(resolve => setTimeout(resolve, 2000)); // Simulate network/processing delay

    const dummyResponses = [
      { identified_object: "Early Blight on Tomato", organic_solution: "Remove infected leaves, ensure good air circulation, apply neem oil spray." },
      { identified_object: "Aphid Infestation", organic_solution: "Spray with insecticidal soap, introduce ladybugs, use strong water spray to dislodge." },
      { identified_object: "Nutrient Deficiency (Nitrogen)", organic_solution: "Apply compost, vermicompost, or well-rotted manure. Use nitrogen-fixing cover crops." },
      { identified_object: "Healthy Plant", organic_solution: "Keep up the good work! Continue with regular organic care practices." },
    ];

    const randomResult = dummyResponses[Math.floor(Math.random() * dummyResponses.length)];

    setResult(randomResult);
    setScanning(false);
  };

  return (
    <section id="scanner" className="container mx-auto p-6 text-center">
      <h2 className="text-4xl font-bold text-green-800 mb-8">{t.aiScanner}</h2>

      <div className="bg-white p-8 rounded-lg shadow-md max-w-2xl mx-auto border border-green-200">
        <p className="text-gray-700 mb-6">{t.scannerPlaceholder}</p>

        <input
          type="file"
          accept="image/*"
          onChange={handleImageChange}
          className="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-green-50 file:text-green-700 hover:file:bg-green-100"
        />

        {previewUrl && (
          <div className="mt-6">
            <img src={previewUrl} alt="Preview" className="max-w-full h-auto rounded-lg shadow-md mx-auto" />
          </div>
        )}

        {error && <p className="text-red-500 mt-4">{error}</p>}

        <button
          onClick={handleScan}
          disabled={!image || scanning}
          className={`mt-6 px-8 py-3 rounded-full text-white font-semibold shadow-lg transition-all ${!image || scanning ? 'bg-gray-400 cursor-not-allowed' : 'bg-green-600 hover:bg-green-700'}`}
        >
          {scanning ? t.scanning : t.scan}
        </button>

        {result && (
          <div className="mt-8 p-6 bg-green-50 border border-green-300 rounded-lg text-left">
            <h3 className="text-2xl font-bold text-green-800 mb-3">{t.scannerResult}</h3>
            <p className="text-gray-800 mb-2"><strong>{t.identifiedObject}:</strong> {result.identified_object}</p>
            <p className="text-gray-800"><strong>{t.organicSolution}:</strong> {result.organic_solution}</p>
          </div>
        )}
      </div>
    </section>
  );
};

const CertificationPage = ({ currentLanguage, isLoggedIn, userDocuments, onFileUpload }) => {
  const t = translations[currentLanguage];
  const [file712, setFile712] = useState(null);
  const [file8A, setFile8A] = useState(null);
  const [uploadMessage, setUploadMessage] = useState('');

  const handleFileChange = (e, type) => {
    if (type === '7_12') {
      setFile712(e.target.files[0]);
    } else if (type === '8A') {
      setFile8A(e.target.files[0]);
    }
  };

  const handleUpload = (type) => {
    let fileToUpload = null;
    if (type === '7_12') {
      fileToUpload = file712;
    } else if (type === '8A') {
      fileToUpload = file8A;
    }

    if (fileToUpload && isLoggedIn) {
      // Simulate file upload
      console.log(`Uploading ${type} file:`, fileToUpload.name);
      onFileUpload(type, fileToUpload.name);
      setUploadMessage(`${fileToUpload.name} ${t.fileUploaded}`);
      // Clear file input after "upload"
      if (type === '7_12') setFile712(null);
      if (type === '8A') setFile8A(null);
      // In a real app, you'd send this file to your backend storage
    } else if (!isLoggedIn) {
      setUploadMessage("Please login to upload documents.");
    } else {
      setUploadMessage("Please select a file to upload.");
    }
    setTimeout(() => setUploadMessage(''), 3000); // Clear message after 3 seconds
  };

  return (
    <section id="certification" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.certificationInfo}</h2>

      <div className="grid md:grid-cols-2 gap-8 mb-10">
        <div className="bg-white p-6 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.certGov}</h3>
          <p className="text-gray-700 mb-3">
            Information on government certifications like National Programme for Organic Production (NPOP) and Participatory Guarantee System for India (PGS-India).
            These are crucial for authenticating organic produce.
          </p>
          <ul className="list-disc list-inside text-gray-700 mb-4">
            <li>NPOP: For export and domestic markets. <a href="https://apeda.gov.in/national-programme-for-organic-production-npop" target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline">APEDA NPOP</a></li>
            <li>PGS-India: Primarily for domestic market, community-based. <a href="https://pgsindia-ncof.gov.in/" target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline">PGS India</a></li>
          </ul>
          <div className="space-y-3">
            {dummyGovCertifications.map(course => (
                <div key={course.id} className="bg-gray-50 p-3 rounded-lg border border-gray-200">
                    <h4 className="font-semibold text-gray-800">{course.title}</h4>
                    <p className="text-sm text-gray-500 mb-1">Provider: {course.provider}</p>
                    <a href={course.url} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline text-sm font-semibold">
                        Visit Site &rarr;
                    </a>
                </div>
            ))}
          </div>
        </div>
        <div className="bg-white p-6 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.certPrivate}</h3>
          <p className="text-gray-700 mb-3">
            Details on private certification bodies, courses, and their standards.
          </p>
          <div className="space-y-3">
              {dummyPrivateCertifications.map(course => (
                  <div key={course.id} className="bg-gray-50 p-3 rounded-lg border border-gray-200">
                      <h4 className="font-semibold text-gray-800">{course.title}</h4>
                      <p className="text-sm text-gray-500 mb-1">Provider: {course.provider}</p>
                      <a href={course.url} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline text-sm font-semibold">
                          Visit Site &rarr;
                      </a>
                  </div>
              ))}
          </div>
        </div>
      </div>

      <div className="bg-white p-6 rounded-lg shadow-md border border-green-200 mb-10">
        <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.certExamModule}</h3>
        <p className="text-gray-700">
          Prepare for organic farming certification exams with our practice modules. These quizzes help you test your knowledge on organic standards and practices.
        </p>
        <button className="mt-4 bg-green-600 hover:bg-green-700 text-white px-5 py-2 rounded-full shadow-md transition-colors">
          Start Practice Exam
        </button>
      </div>

      <div className="bg-white p-6 rounded-lg shadow-md border border-green-200 mb-10">
        <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.onlineCourses}</h3>
        <div className="grid md:grid-cols-2 gap-4">
          {dummyCourses.map(course => (
            <div key={course.id} className="bg-gray-50 p-4 rounded-lg border border-gray-200 hover:shadow-md transition-shadow">
              <h4 className="text-lg font-bold text-gray-800">{course.title}</h4>
              <p className="text-sm text-gray-600 mb-2">Provider: {course.provider}</p>
              <a href={course.url} target="_blank" rel="noopener noreferrer" className="text-blue-600 hover:underline font-semibold">
                Go to Course &rarr;
              </a>
            </div>
          ))}
        </div>
      </div>

      {isLoggedIn && (
        <div className="bg-white p-6 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.uploadCertificates}</h3>
          <p className="text-gray-600 mb-4 text-sm">{t.fileUploadDisclaimer}</p>

          <div className="grid md:grid-cols-2 gap-6">
            <div>
              <label htmlFor="712-upload" className="block text-gray-700 text-lg font-medium mb-2">{t.upload712}</label>
              <input
                type="file"
                id="712-upload"
                accept=".pdf"
                onChange={(e) => handleFileChange(e, '7_12')}
                className="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"
              />
              <button
                onClick={() => handleUpload('7_12')}
                disabled={!file712}
                className={`mt-3 px-6 py-2 rounded-full text-white font-semibold shadow-md transition-colors ${!file712 ? 'bg-gray-400 cursor-not-allowed' : 'bg-blue-600 hover:bg-blue-700'}`}
              >
                {t.upload} 7/12
              </button>
            </div>
            <div>
              <label htmlFor="8a-upload" className="block text-gray-700 text-lg font-medium mb-2">{t.upload8A}</label>
              <input
                type="file"
                id="8a-upload"
                accept=".pdf"
                onChange={(e) => handleFileChange(e, '8A')}
                className="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"
              />
              <button
                onClick={() => handleUpload('8A')}
                disabled={!file8A}
                className={`mt-3 px-6 py-2 rounded-full text-white font-semibold shadow-md transition-colors ${!file8A ? 'bg-gray-400 cursor-not-allowed' : 'bg-blue-600 hover:bg-blue-700'}`}
              >
                {t.upload} 8A
              </button>
            </div>
          </div>
          {uploadMessage && <p className="mt-4 text-center text-green-600 font-semibold">{uploadMessage}</p>}

          <div className="mt-8">
            <h4 className="text-xl font-semibold text-gray-800 mb-3">{t.userDocuments}</h4>
            {userDocuments.length > 0 ? (
              <div className="overflow-x-auto">
                <table className="min-w-full bg-white border border-gray-200 rounded-lg shadow-sm">
                  <thead>
                    <tr className="bg-gray-100 text-left text-gray-600 text-sm uppercase tracking-wider">
                      <th className="py-3 px-4 border-b">{t.documentType}</th>
                      <th className="py-3 px-4 border-b">{t.fileName}</th>
                      <th className="py-3 px-4 border-b">{t.uploadedOn}</th>
                      <th className="py-3 px-4 border-b">{t.status}</th>
                      <th className="py-3 px-4 border-b">{t.download}</th>
                    </tr>
                  </thead>
                  <tbody>
                    {userDocuments.map((doc, index) => (
                      <tr key={index} className="border-b border-gray-200 hover:bg-gray-50">
                        <td className="py-3 px-4 text-gray-800">{doc.type === '7_12' ? '7/12 Extract' : '8A Extract'}</td>
                        <td className="py-3 px-4 text-gray-800">{doc.name}</td>
                        <td className="py-3 px-4 text-gray-800">{doc.uploadedAt}</td>
                        <td className="py-3 px-4">
                          <span className={`px-3 py-1 text-xs font-semibold rounded-full ${doc.verified ? 'bg-green-200 text-green-800' : 'bg-yellow-200 text-yellow-800'}`}>
                            {doc.verified ? t.verified : t.pending}
                          </span>
                        </td>
                        <td className="py-3 px-4">
                          <a href="#" className="text-blue-600 hover:underline">{t.download}</a>
                        </td>
                      </tr>
                    ))}
                  </tbody>
                </table>
              </div>
            ) : (
              <p className="text-gray-600 text-center">{t.noDocuments}</p>
            )}
          </div>
        </div>
      )}
    </section>
  );
};

const LoginPage = ({ currentLanguage, onLogin }) => {
  const t = translations[currentLanguage];
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    setError('');

    if (!email) {
      setError(t.emailRequired);
      return;
    }
    if (!password) {
      setError(t.passwordRequired);
      return;
    }

    // Simulate login (replace with actual API call to backend)
    if (email === 'test@example.com' && password === 'password123') {
      onLogin(email);
      window.location.hash = '#dashboard'; // Redirect to dashboard on success
    } else {
      setError(t.loginFailed);
    }
  };

  return (
    <section id="login" className="container mx-auto p-6 flex justify-center items-center min-h-[60vh]">
      <div className="bg-white p-8 rounded-lg shadow-md w-full max-w-md border border-green-200">
        <h2 className="text-3xl font-bold text-green-800 mb-6 text-center">{t.login}</h2>
        <form onSubmit={handleSubmit}>
          <div className="mb-4">
            <label htmlFor="email" className="block text-gray-700 text-sm font-bold mb-2">{t.email}:</label>
            <input
              type="email"
              id="email"
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
              required
            />
          </div>
          <div className="mb-6">
            <label htmlFor="password" className="block text-gray-700 text-sm font-bold mb-2">{t.password}:</label>
            <input
              type="password"
              id="password"
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              required
            />
          </div>
          {error && <p className="text-red-500 text-xs italic mb-4">{error}</p>}
          <div className="flex items-center justify-between">
            <button
              type="submit"
              className="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-6 rounded-full focus:outline-none focus:shadow-outline shadow-md transition-colors"
            >
              {t.login}
            </button>
            <a href="#register" className="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800">
              {t.register}?
            </a>
          </div>
        </form>
      </div>
    </section>
  );
};

const RegisterPage = ({ currentLanguage, onRegister }) => {
  const t = translations[currentLanguage];
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [confirmPassword, setConfirmPassword] = useState('');
  const [farmerId, setFarmerId] = useState('');
  const [error, setError] = useState('');
  const [success, setSuccess] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    setError('');
    setSuccess('');

    if (!email) { setError(t.emailRequired); return; }
    if (!/\S+@\S+\.\S+/.test(email)) { setError(t.invalidEmail); return; }
    if (!password) { setError(t.passwordRequired); return; }
    if (password.length < 6) { setError(t.passwordMinLength); return; }
    if (password !== confirmPassword) { setError(t.passwordsMismatch); return; }

    // Simulate registration (replace with actual API call to backend)
    // IMPORTANT: In a real app, Farmer ID is NOT the password.
    // It would be an optional field for linking/verification after registration.
    if (email && password === confirmPassword) {
      onRegister(email, farmerId);
      setSuccess(t.registerSuccess);
      setEmail('');
      setPassword('');
      setConfirmPassword('');
      setFarmerId('');
      window.location.hash = '#login'; // Redirect to login on success
    } else {
      setError(t.registerFailed);
    }
  };

  return (
    <section id="register" className="container mx-auto p-6 flex justify-center items-center min-h-[60vh]">
      <div className="bg-white p-8 rounded-lg shadow-md w-full max-w-md border border-green-200">
        <h2 className="text-3xl font-bold text-green-800 mb-6 text-center">{t.register}</h2>
        <form onSubmit={handleSubmit}>
          <div className="mb-4">
            <label htmlFor="reg-email" className="block text-gray-700 text-sm font-bold mb-2">{t.email}:</label>
            <input
              type="email"
              id="reg-email"
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
              required
            />
          </div>
          <div className="mb-4">
            <label htmlFor="reg-password" className="block text-gray-700 text-sm font-bold mb-2">{t.password}:</label>
            <input
              type="password"
              id="reg-password"
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              required
            />
          </div>
          <div className="mb-4">
            <label htmlFor="confirm-password" className="block text-gray-700 text-sm font-bold mb-2">{t.confirmPassword}:</label>
            <input
              type="password"
              id="confirm-password"
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500"
              value={confirmPassword}
              onChange={(e) => setConfirmPassword(e.target.value)}
              required
            />
          </div>
          <div className="mb-6">
            <label htmlFor="farmer-id" className="block text-gray-700 text-sm font-bold mb-2">{t.farmerIdOptional}:</label>
            <input
              type="text"
              id="farmer-id"
              className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500"
              value={farmerId}
              onChange={(e) => setFarmerId(e.target.value)}
            />
          </div>
          {error && <p className="text-red-500 text-xs italic mb-4">{error}</p>}
          {success && <p className="text-green-600 text-xs italic mb-4">{success}</p>}
          <div className="flex items-center justify-between">
            <button
              type="submit"
              className="bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-6 rounded-full focus:outline-none focus:shadow-outline shadow-md transition-colors"
            >
              {t.register}
            </button>
            <a href="#login" className="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800">
              {t.login}?
            </a>
          </div>
        </form>
      </div>
    </section>
  );
};

const UserDashboard = ({ currentLanguage, userEmail, userDocuments }) => {
  const t = translations[currentLanguage];
  return (
    <section id="dashboard" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">User Dashboard</h2>
      <div className="bg-white p-8 rounded-lg shadow-md border border-green-200">
        <h3 className="text-2xl font-semibold text-gray-800 mb-4">Welcome, {userEmail}!</h3>
        <p className="text-gray-700 mb-6">This is your personalized dashboard. Here you can manage your profile, view uploaded documents, and track your activities.</p>

        <h4 className="text-xl font-semibold text-gray-800 mb-3">{t.userDocuments}</h4>
        {userDocuments.length > 0 ? (
          <div className="overflow-x-auto">
            <table className="min-w-full bg-white border border-gray-200 rounded-lg shadow-sm">
              <thead>
                <tr className="bg-gray-100 text-left text-gray-600 text-sm uppercase tracking-wider">
                  <th className="py-3 px-4 border-b">{t.documentType}</th>
                  <th className="py-3 px-4 border-b">{t.fileName}</th>
                  <th className="py-3 px-4 border-b">{t.uploadedOn}</th>
                  <th className="py-3 px-4 border-b">{t.status}</th>
                  <th className="py-3 px-4 border-b">{t.download}</th>
                </tr>
              </thead>
              <tbody>
                {userDocuments.map((doc, index) => (
                  <tr key={index} className="border-b border-gray-200 hover:bg-gray-50">
                    <td className="py-3 px-4 text-gray-800">{doc.type === '7_12' ? '7/12 Extract' : '8A Extract'}</td>
                    <td className="py-3 px-4 text-gray-800">{doc.name}</td>
                    <td className="py-3 px-4 text-gray-800">{doc.uploadedAt}</td>
                    <td className="py-3 px-4">
                          <span className={`px-3 py-1 text-xs font-semibold rounded-full ${doc.verified ? 'bg-green-200 text-green-800' : 'bg-yellow-200 text-yellow-800'}`}>
                            {doc.verified ? t.verified : t.pending}
                          </span>
                    </td>
                    <td className="py-3 px-4">
                      <a href="#" className="text-blue-600 hover:underline">{t.download}</a>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        ) : (
          <p className="text-gray-600 text-center">{t.noDocuments}</p>
        )}
      </div>
    </section>
  );
};

const ContactPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [formData, setFormData] = useState({ name: '', email: '', subject: '', message: '' });
  const [status, setStatus] = useState('');

  const handleChange = (e) => {
    const { id, value } = e.target;
    setFormData(prevData => ({ ...prevData, [id]: value }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setStatus('sending');

    // **IMPORTANT**: This is a placeholder URL.
    // Replace this with the actual URL of your deployed backend service.
    const backendUrl = 'https://your-live-backend-api.com/send-message';

    try {
      // Attempt to send the form data to your backend
      const response = await fetch(backendUrl, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(formData),
      });

      if (response.ok) {
        // This means the backend received the data successfully
        setStatus('success');
        setFormData({ name: '', email: '', subject: '', message: '' });
      } else {
        // This means the backend responded with an error (e.g., validation failed)
        setStatus('error');
      }
    } catch (error) {
      // This catches network errors (e.g., the backend server is down or the URL is wrong)
      console.error('Failed to send message:', error);
      // We show a generic error to the user as the backend is not live yet.
      setStatus('error');
    }
  };

  return (
    <section id="contact" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.contactUs}</h2>
      <div className="grid md:grid-cols-2 gap-10">
        {/* Contact Info */}
        <div className="bg-white p-8 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-gray-800 mb-4">{t.contactInfo}</h3>
          <p className="text-gray-700 mb-4">
            Have questions about organic farming, our platform, or just want to say hello? Reach out to us through any of the methods below.
          </p>
          <div className="space-y-4">
            <p className="flex items-center text-lg">
              <svg className="w-6 h-6 mr-3 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path></svg>
              <a href={`mailto:${t.emailAddress}`} className="text-blue-600 hover:underline">{t.emailAddress}</a>
            </p>
            <p className="flex items-center text-lg">
              <svg className="w-6 h-6 mr-3 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path></svg>
              <a href={`tel:${t.phoneNumber}`} className="text-blue-600 hover:underline">{t.phoneNumber}</a>
            </p>
          </div>
        </div>

        {/* Contact Form */}
        <div className="bg-white p-8 rounded-lg shadow-md border border-green-200">
          <form onSubmit={handleSubmit}>
            <div className="mb-4">
              <label htmlFor="name" className="block text-gray-700 text-sm font-bold mb-2">{t.yourName}:</label>
              <input type="text" id="name" value={formData.name} onChange={handleChange} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500" required />
            </div>
            <div className="mb-4">
              <label htmlFor="email" className="block text-gray-700 text-sm font-bold mb-2">{t.email}:</label>
              <input type="email" id="email" value={formData.email} onChange={handleChange} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500" required />
            </div>
            <div className="mb-4">
              <label htmlFor="subject" className="block text-gray-700 text-sm font-bold mb-2">{t.subject}:</label>
              <input type="text" id="subject" value={formData.subject} onChange={handleChange} className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500" />
            </div>
            <div className="mb-6">
              <label htmlFor="message" className="block text-gray-700 text-sm font-bold mb-2">{t.message}:</label>
              <textarea id="message" value={formData.message} onChange={handleChange} rows="5" className="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline focus:border-green-500" required></textarea>
            </div>
            <div className="text-center">
              <button type="submit" disabled={status === 'sending'} className="bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-8 rounded-full focus:outline-none focus:shadow-outline shadow-md transition-colors disabled:bg-gray-400">
                {status === 'sending' ? 'Sending...' : t.sendMessage}
              </button>
            </div>
            {status === 'success' && <p className="mt-4 text-center text-green-600 font-semibold">{t.messageSentSuccess}</p>}
            {status === 'error' && <p className="mt-4 text-center text-red-500 font-semibold">{t.messageSentError}</p>}
          </form>
        </div>
      </div>
    </section>
  );
};

const WeatherAdvisoryPage = ({ currentLanguage }) => {
  const t = translations[currentLanguage];
  const [weatherData, setWeatherData] = useState(null);

  useEffect(() => {
    // Simulate fetching weather data
    setWeatherData(dummyWeatherData);
  }, []);

  const WeatherIcon = ({ iconName, className }) => {
    const icons = {
      "sun": <svg xmlns="http://www.w3.org/2000/svg" className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" /></svg>,
      "cloudy": <svg xmlns="http://www.w3.org/2000/svg" className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M3 15a4 4 0 004 4h9a5 5 0 10-.1-9.999 5.002 5.002 0 10-9.78 2.096A4.001 4.001 0 003 15z" /></svg>,
      "sun-cloud": <svg xmlns="http://www.w3.org/2000/svg" className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M12 5c2.4 0 4.6.8 6.4 2.2-1 .3-1.9.8-2.7 1.5l-.2.2c-2.4 2.4-6.2 2.4-8.7 0l-.2-.2c-.8-.7-1.7-1.2-2.7-1.5C7.4 5.8 9.6 5 12 5zm0 0a7 7 0 017 7c0 1.6-.5 3-1.4 4.2m-11.2 0A7 7 0 015 12c0-1.6.5-3 1.4-4.2M12 15c-2.2 0-4-1.8-4-4s1.8-4 4-4 4 1.8 4 4-1.8 4-4 4zm0 0a4 4 0 01-4-4h8a4 4 0 01-4 4z" /></svg>,
      "rain": <svg xmlns="http://www.w3.org/2000/svg" className={className} fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M12 14v7m-4-5l-1 1m8-1l1 1" /></svg>,
    };
    return icons[iconName] || icons['cloudy'];
  };
  
  const getAdvisory = () => {
      const hasRain = weatherData.forecast.some(day => day.condition.en.toLowerCase().includes('rain'));
      const isHot = weatherData.forecast.some(day => day.maxtemp_c > 32);

      if (hasRain) return t.advisoryRain;
      if (isHot) return t.advisoryHot;
      return t.advisoryMixed;
  };

  if (!weatherData) return <p>Loading weather data...</p>;

  return (
    <section id="weather" className="container mx-auto p-6">
      <h2 className="text-4xl font-bold text-green-800 mb-8 text-center">{t.weatherAdvisory}</h2>

      <div className="grid lg:grid-cols-3 gap-8 mb-10">
        {/* Current Weather */}
        <div className="lg:col-span-1 bg-white p-6 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.currentWeather}</h3>
          <p className="text-gray-600 mb-4 text-lg">{weatherData.current.location}</p>
          <div className="flex items-center justify-center space-x-4 mb-4">
            <div className="text-yellow-500">
              <WeatherIcon iconName={weatherData.current.icon} className="w-24 h-24" />
            </div>
            <div>
              <p className="text-6xl font-bold text-gray-800">{weatherData.current.temp_c}°C</p>
              <p className="text-gray-700 text-center">{weatherData.current.condition[currentLanguage]}</p>
            </div>
          </div>
          <div className="flex justify-around text-center text-gray-700">
            <div>
              <p className="font-semibold">{t.humidity}</p>
              <p>{weatherData.current.humidity}%</p>
            </div>
            <div>
              <p className="font-semibold">{t.wind}</p>
              <p>{weatherData.current.wind_kph} km/h</p>
            </div>
          </div>
        </div>

        {/* 5-Day Forecast */}
        <div className="lg:col-span-2 bg-white p-6 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-green-700 mb-4">{t.forecast}</h3>
          <div className="flex justify-between space-x-2">
            {weatherData.forecast.map((day, index) => (
              <div key={index} className="flex-1 text-center bg-green-50 p-3 rounded-lg border border-green-100">
                <p className="font-bold text-gray-800">{day.day[currentLanguage]}</p>
                <p className="text-sm text-gray-500">{day.date}</p>
                <div className="my-2 text-yellow-600">
                   <WeatherIcon iconName={day.icon} className="w-12 h-12 mx-auto" />
                </div>
                <p className="text-lg font-semibold">{day.maxtemp_c}°</p>
                <p className="text-sm text-gray-600">{day.mintemp_c}°</p>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Agricultural Advisory */}
      <div className="bg-white p-6 rounded-lg shadow-md border border-green-200">
          <h3 className="text-2xl font-semibold text-green-700 mb-4 flex items-center">
            <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6 mr-3" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
            {t.agriAdvisory}
          </h3>
          <p className="text-gray-700 leading-relaxed">
            {getAdvisory()}
          </p>
      </div>
    </section>
  );
};


// --- Main App Component ---
function App() {
  const [language, setLanguage] = useState('en');
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [userEmail, setUserEmail] = useState('');
  const [userDocuments, setUserDocuments] = useState([]); // { type: '7_12'/'8A', name: 'filename.pdf', uploadedAt: 'date', verified: false }
  const [route, setRoute] = useState(window.location.hash.substring(1) || 'home');

  useEffect(() => {
    // Check for logged-in user from session/localStorage in a real app
    const storedUser = localStorage.getItem('currentUser');
    if (storedUser) {
      setIsLoggedIn(true);
      setUserEmail(storedUser);
      const storedDocs = JSON.parse(localStorage.getItem('userDocuments')) || [];
      setUserDocuments(storedDocs);
    }

    // Handle hash changes for navigation
    const handleHashChange = () => {
      // By setting state, we ensure a re-render happens, which is the correct React pattern.
      setRoute(window.location.hash.substring(1) || 'home');
    };

    window.addEventListener('hashchange', handleHashChange);

    return () => {
      window.removeEventListener('hashchange', handleHashChange);
    };
  }, []);

  const handleLogin = (email) => {
    setIsLoggedIn(true);
    setUserEmail(email);
    localStorage.setItem('currentUser', email); // Simulate login
    // In a real app, fetch user documents from backend here
    const storedDocs = JSON.parse(localStorage.getItem('userDocuments')) || [];
    setUserDocuments(storedDocs);
    alert(translations[language].loginSuccess);
  };

  const handleRegister = (email, farmerId) => {
    // In a real app, this would send data to backend for user creation
    console.log("Simulating registration for:", email, "Farmer ID:", farmerId);
    alert(translations[language].registerSuccess);
  };

  const handleLogout = () => {
    setIsLoggedIn(false);
    setUserEmail('');
    setUserDocuments([]);
    localStorage.removeItem('currentUser'); // Simulate logout
    localStorage.removeItem('userDocuments');
    window.location.hash = '#'; // Redirect to home
  };

  const handleFileUpload = (type, fileName) => {
    const newDoc = {
      type: type,
      name: fileName,
      uploadedAt: new Date().toLocaleDateString(language),
      verified: false // Always false for simulated upload
    };
    setUserDocuments(prevDocs => {
      const updatedDocs = [...prevDocs, newDoc];
      localStorage.setItem('userDocuments', JSON.stringify(updatedDocs)); // Simulate storage
      return updatedDocs;
    });
  };

  const renderPage = () => {
    switch (route) {
      case 'schemes':
        return <SchemesPage currentLanguage={language} />;
      case 'products':
        return <ProductsPage currentLanguage={language} />;
      case 'learning':
        return <LearningPage currentLanguage={language} />;
      case 'awards':
        return <AwardsPage currentLanguage={language} />;
      case 'demand':
        return <MarketDemandPage currentLanguage={language} />;
      case 'scanner':
        return <AIScannerPage currentLanguage={language} />;
      case 'certification':
        return <CertificationPage currentLanguage={language} isLoggedIn={isLoggedIn} userDocuments={userDocuments} onFileUpload={handleFileUpload} />;
      case 'weather':
        return <WeatherAdvisoryPage currentLanguage={language} />;
      case 'login':
        return <LoginPage currentLanguage={language} onLogin={handleLogin} />;
      case 'register':
        return <RegisterPage currentLanguage={language} onRegister={handleRegister} />;
      case 'dashboard':
        return isLoggedIn ? <UserDashboard currentLanguage={language} userEmail={userEmail} userDocuments={userDocuments} /> : <LoginPage currentLanguage={language} onLogin={handleLogin} />;
      case 'contact':
        return <ContactPage currentLanguage={language} />;
      default:
        return <HomePage currentLanguage={language} />;
    }
  };

  return (
    <div className="min-h-screen flex flex-col font-sans bg-gray-50">
      <style>
        {`
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
        body {
          font-family: 'Inter', sans-serif;
        }
        .container {
          max-width: 1200px;
        }
        .app-header {
          position: sticky;
          top: 0;
          z-index: 1000;
        }
        .nav-links li a, .auth-links a {
          padding: 8px 12px;
          border-radius: 9999px; /* Tailwind rounded-full */
        }
        .nav-links li a:hover, .auth-links a:hover {
          background-color: rgba(255, 255, 255, 0.1);
        }
        .best-price {
          background-color: #fefcbf; /* Tailwind yellow-100 */
          border-color: #fcd34d; /* Tailwind yellow-400 */
        }
        .badge {
          display: inline-block;
          padding: 0.25em 0.6em;
          font-size: 75%;
          font-weight: 700;
          line-height: 1;
          text-align: center;
          white-space: nowrap;
          vertical-align: baseline;
          border-radius: 0.375rem; /* Tailwind rounded-md */
        }
        .animate-fade-in-down {
          animation: fadeInDown 1s ease-out;
        }
        .animate-fade-in-up {
          animation: fadeInUp 1s ease-out;
        }
        @keyframes fadeInDown {
          from { opacity: 0; transform: translateY(-20px); }
          to { opacity: 1; transform: translateY(0); }
        }
        @keyframes fadeInUp {
          from { opacity: 0; transform: translateY(20px); }
          to { opacity: 1; transform: translateY(0); }
        }
        /* Leaflet CSS loaded via CDN */
        @import url('https://unpkg.com/leaflet@1.7.1/dist/leaflet.css');
        `}
      </style>
      {/* Load Leaflet JavaScript globally */}
      <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>

      <Header
        onLanguageChange={setLanguage}
        currentLanguage={language}
        isLoggedIn={isLoggedIn}
        onLogout={handleLogout}
      />
      <main className="flex-grow">
        {renderPage()}
      </main>
      <Footer currentLanguage={language} />
    </div>
  );
}

export default App;
    
</body>
</html>
