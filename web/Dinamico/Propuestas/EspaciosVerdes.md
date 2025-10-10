<div style="text-align:center;">
<img src="https://raw.githubusercontent.com/Tarikul-Islam-Anik/Animated-Fluent-Emojis/master/Emojis/People%20with%20activities/Man%20Mountain%20Biking%20Medium%20Skin%20Tone.png" alt="Man Technologist Medium-Dark Skin Tone" width="180px" />
</div>

 <!-- <div class="vocaroo-container">
        <iframe width="300" height="60" src="https://vocaroo.com/embed/1bfn2LKLm9JE?autoplay=1" frameborder="0" allow="autoplay"></iframe>
    </div> -->

# Leyes para Fomentar los Espacios Verdes.
## Interiorizar
Como seres vivientes nos enfermamos de estrés sin darnos cuenta: la falta de verde nos aísla, nos pone irritables y nos quita conexión con la naturaleza. Los parques y árboles no son lujo: regulan la temperatura, refrescan el aire y nos ayudan a mantener la cabeza clara. Por eso hacen falta leyes que obliguen a tenerlos, no solo para embellecer, sino para que nuestra salud mental y física sobreviva al calor y al concreto.

# 🌳 Por mas Espacios Verdes

<div class="gallery-container">
    <div class="contenedor-imagenes-animado" >
        {"image": "https://i.ibb.co/VY0KXm8g/image.png", "link": "https://www.instagram.com/fottograma/"},
        {"image": "https://i.ibb.co/tw4j19Bx/image.png", "link": "https://www.instagram.com/fottograma/"},
        {"image": "https://i.ibb.co/mrtX74GM/image.png", "link": "https://www.instagram.com/fottograma/"},
        {"image": "https://i.ibb.co/7JcLTJCz/image.png", "link": "https://www.instagram.com/fottograma/"},
        {"image": "https://i.ibb.co/JWBT1Ych/image.png", "link": "https://www.instagram.com/fottograma/"}
    </div>
</div>


















# Relacionado 
[Ley Ambiental](web\Dinamico\Propuestas\Ambiente.md) · [Ley Salud Mental](web\Dinamico\Propuestas\SaludMental.md) 


<!-- > Scrips de Galeria </-->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/Swiper/8.4.5/swiper-bundle.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Swiper/8.4.5/swiper-bundle.min.js"></script>

<script>

async function loadGalleryData() {
    try {
        const response = await fetch('web/Dinamico/data.json');
        const data = await response.json();
        return data.galleries;
    } catch (error) {
        return null;
    }
}

function createSwiper(container, images) {
    container.innerHTML = `
        <div class="swiper-wrapper">
            ${images.map(item => `
                <div class="swiper-slide">
                    <a href="${item.link}">
                        <img src="${item.image}" alt="${item.name || 'Imagen'}" loading="lazy" />
                    </a>
                </div>
            `).join('')}
        </div>
    `;

    return new Swiper(container, {
        slidesPerView: 'auto',
        spaceBetween: 20,
        loop: true,
        centeredSlides: true,
        autoplay: {
            delay: 3000,
            disableOnInteraction: false,
        }
    });
}

function parseInlineGalleryData(element) {
    try {
        const content = element.textContent.trim();
        if (!content) return null;
        const jsonStr = `[${content}]`;
        return { images: JSON.parse(jsonStr) };
    } catch (error) {
        return null;
    }
}

async function initializeAllGalleries() {
    if (typeof Swiper === 'undefined') {
        return;
    }
    
    const allGalleryData = await loadGalleryData();
    
    if (allGalleryData) {
        const galleryElements = document.querySelectorAll('[id$="-gallery"]');
        
        galleryElements.forEach(container => {
            const galleryId = container.id.replace('-gallery', '');
            
            const matchingKey = Object.keys(allGalleryData).find(key => 
                key.toLowerCase() === galleryId.toLowerCase()
            );
            
            if (matchingKey && allGalleryData[matchingKey].images?.length > 0) {
                container.classList.add('swiper');
                createSwiper(container, allGalleryData[matchingKey].images);
            }
        });
    } else {
        return;
    }

    const inlineGalleries = document.querySelectorAll('.contenedor-imagenes-animado:not([id])');
    
    inlineGalleries.forEach(async (container) => {
        const inlineData = parseInlineGalleryData(container);
        if (inlineData) {
            container.classList.add('swiper');
            createSwiper(container, inlineData.images);
        }
    });
}

function waitForSwiperAndInit() {
    if (typeof Swiper !== 'undefined') {
        initializeAllGalleries();
    } else {
        setTimeout(waitForSwiperAndInit, 100);
    }
}

waitForSwiperAndInit();
</script>