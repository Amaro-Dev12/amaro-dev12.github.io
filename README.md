# amaro-dev12.github.io
import React, { useState } from 'react';
import { Search, Bug, Sprout, AlertCircle, MapPin, Filter } from 'lucide-react';

const PestControlDB = () => {
  const [searchTerm, setSearchTerm] = useState('');
  const [selectedPest, setSelectedPest] = useState(null);
  const [selectedRegion, setSelectedRegion] = useState('Todas');
  const [showFilters, setShowFilters] = useState(false);

  // Base de datos ampliada de plagas
  const pestDatabase = [
    {
      id: 1,
      name: 'Mosca blanca',
      scientificName: 'Bemisia tabaci / Trialeurodes vaporariorum',
      description: 'Pequeñas moscas blancas que succionan la savia y debilitan las plantas, transmiten virus',
      regions: ['Andalucía', 'Canarias y Baleares'],
      crops: ['Tomate', 'Pepino', 'Calabacín', 'Berenjena', 'Pimiento', 'Melón'],
      products: [
        { name: 'Spiromesifen', type: 'Químico', dosage: '1 ml/L' },
        { name: 'Trampas amarillas', type: 'Físico', dosage: '1 trampa/10m²' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2 g/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '1-2% en agua' },
        { name: 'Eretmocerus mundus', type: 'Control biológico', dosage: '5 ind/m²' }
      ]
    },
    {
      id: 2,
      name: 'Trips occidental de las flores',
      scientificName: 'Frankliniella occidentalis',
      description: 'Insecto diminuto que daña flores, frutos y hojas, transmite virus',
      regions: ['Andalucía', 'Murcia y C. Valenciana', 'Canarias y Baleares', 'Galicia, Asturias y Cantabria'],
      crops: ['Pimiento', 'Tomate', 'Pepino', 'Sandía', 'Flores ornamentales', 'Hortalizas'],
      products: [
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas azules', type: 'Físico', dosage: '1 trampa/20m²' },
        { name: 'Orius laevigatus', type: 'Control biológico', dosage: '5 ind/m²' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 3,
      name: 'Polilla del tomate (Tuta)',
      scientificName: 'Tuta absoluta',
      description: 'Larva que perfora hojas, tallos y frutos causando graves daños',
      regions: ['Andalucía', 'Canarias y Baleares'],
      crops: ['Tomate', 'Berenjena', 'Patata', 'Pimiento'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorantraniliprol', type: 'Químico', dosage: '0.3 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '1 trampa/500m²' },
        { name: 'Nesidiocoris tenuis', type: 'Control biológico', dosage: '1-2 ind/m²' }
      ]
    },
    {
      id: 4,
      name: 'Pulgón del algodón',
      scientificName: 'Aphis gossypii',
      description: 'Pulgón pequeño de color variable, muy polífago y transmisor de virus',
      regions: ['Andalucía'],
      crops: ['Algodón', 'Pepino', 'Melón', 'Sandía', 'Calabacín', 'Hortalizas diversas'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '1-2% en agua' },
        { name: 'Acetamiprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' },
        { name: 'Aphidius colemani', type: 'Control biológico', dosage: '1-2 ind/m²' }
      ]
    },
    {
      id: 5,
      name: 'Pulgón verde del melocotonero',
      scientificName: 'Myzus persicae',
      description: 'Pulgón verde amarillento que ataca gran variedad de cultivos, transmite virus',
      regions: ['Andalucía', 'Murcia y C. Valenciana', 'Galicia, Asturias y Cantabria'],
      crops: ['Melocotonero', 'Pimiento', 'Tomate', 'Lechuga', 'Patata', 'Hortalizas'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '1-2% en agua' },
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' },
        { name: 'Aphidius colemani', type: 'Control biológico', dosage: '1-2 ind/m²' }
      ]
    },
    {
      id: 6,
      name: 'Mosca minadora',
      scientificName: 'Liriomyza trifolii / L. huidobrensis',
      description: 'Larva que crea galerías sinuosas en las hojas reduciendo la fotosíntesis',
      regions: ['Andalucía'],
      crops: ['Pepino', 'Judía', 'Melón', 'Tomate', 'Apio', 'Lechuga'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Azadiractina', type: 'Ecológico', dosage: '3 ml/L' },
        { name: 'Diglyphus isaea', type: 'Control biológico', dosage: '3-5 ind/m²' },
        { name: 'Trampas amarillas', type: 'Físico', dosage: '1 trampa/25m²' }
      ]
    },
    {
      id: 7,
      name: 'Barrenillo del olivo',
      scientificName: 'Phloeotribus scarabaeoides',
      description: 'Pequeño escarabajo que perfora galerías bajo la corteza del olivo',
      regions: ['Andalucía', 'Castilla-La Mancha'],
      crops: ['Olivar'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Poda de ramas afectadas', type: 'Cultural', dosage: 'Eliminación y quema' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '2-4 trampas/ha' }
      ]
    },
    {
      id: 8,
      name: 'Mosca del olivo',
      scientificName: 'Bactrocera oleae',
      description: 'Mosca que deposita huevos en la aceituna, larva devora la pulpa',
      regions: ['Andalucía', 'Castilla-La Mancha'],
      crops: ['Olivar'],
      products: [
        { name: 'Trampas con atrayente', type: 'Físico', dosage: '1 trampa/árbol' },
        { name: 'Dimetoato', type: 'Químico', dosage: '1.5 ml/L' },
        { name: 'Spinosad (cebo)', type: 'Biológico', dosage: 'Aplicación localizada' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2 g/L' }
      ]
    },
    {
      id: 9,
      name: 'Mosca de la fruta',
      scientificName: 'Ceratitis capitata',
      description: 'Mosca que ataca frutos maduros, larva se alimenta de la pulpa',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos', 'Caqui', 'Melocotón', 'Albaricoque', 'Higuera'],
      products: [
        { name: 'Trampas con atrayente', type: 'Físico', dosage: '20-40 trampas/ha' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Spinosad (cebo)', type: 'Biológico', dosage: 'Aplicación en bandas' },
        { name: 'Trampeo masivo', type: 'Físico', dosage: '60-80 trampas/ha' }
      ]
    },
    {
      id: 10,
      name: 'Piojo rojo de California',
      scientificName: 'Aonidiella aurantii',
      description: 'Cochinilla que forma colonias densas en frutos, ramas y hojas',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Aphytis melinus', type: 'Control biológico', dosage: 'Suelta periódica' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' }
      ]
    },
    {
      id: 11,
      name: 'Minador de los cítricos',
      scientificName: 'Phyllocnistis citrella',
      description: 'Larva que crea galerías serpentiformes en hojas jóvenes de cítricos',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos jóvenes', 'Viveros'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aceite de parafina', type: 'Ecológico', dosage: '1% en agua' },
        { name: 'Azadiractina', type: 'Ecológico', dosage: '3 ml/L' }
      ]
    },
    {
      id: 12,
      name: 'Cochinilla acanalada',
      scientificName: 'Planococcus citri / Saissetia oleae',
      description: 'Insectos recubiertos de cera que succionan savia y producen melaza',
      regions: ['Murcia y C. Valenciana', 'Canarias y Baleares'],
      crops: ['Cítricos', 'Olivo', 'Ornamentales'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' }
      ]
    },
    {
      id: 13,
      name: 'Polilla del racimo',
      scientificName: 'Lobesia botrana',
      description: 'Oruga que ataca yemas, flores y frutos de la vid',
      regions: ['Murcia y C. Valenciana', 'Castilla-La Mancha', 'Cataluña y Aragón'],
      crops: ['Viñedos'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Confusión sexual', type: 'Físico', dosage: '500 difusores/ha' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo' }
      ]
    },
    {
      id: 14,
      name: 'Mosquito verde del viñedo',
      scientificName: 'Empoasca vitis',
      description: 'Cicadélido que succiona savia causando enrollamiento de hojas',
      regions: ['Castilla-La Mancha'],
      crops: ['Viñedos'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' },
        { name: 'Control biológico natural', type: 'Cultural', dosage: 'Fomentar enemigos naturales' }
      ]
    },
    {
      id: 15,
      name: 'Gorgojo del cereal',
      scientificName: 'Sitophilus granarius',
      description: 'Escarabajo que perfora granos de cereal en almacenamiento',
      regions: ['Castilla-La Mancha', 'Castilla y León'],
      crops: ['Trigo', 'Cebada', 'Maíz almacenado'],
      products: [
        { name: 'Fosfina', type: 'Químico', dosage: 'Fumigación profesional' },
        { name: 'Tierra de diatomeas', type: 'Ecológico', dosage: '1 kg/tonelada' },
        { name: 'Control de temperatura', type: 'Físico', dosage: 'Refrigeración <15°C' }
      ]
    },
    {
      id: 16,
      name: 'Langosta mediterránea',
      scientificName: 'Locusta migratoria / Dociostaurus maroccanus',
      description: 'Saltamontes que puede formar plagas devastadoras en cultivos extensivos',
      regions: ['Castilla-La Mancha'],
      crops: ['Cereales', 'Pastizales', 'Cultivos herbáceos'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2-3 ml/L' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2-3 g/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' }
      ]
    },
    {
      id: 17,
      name: 'Pulgón del trigo',
      scientificName: 'Metopolophium dirhodum',
      description: 'Pulgón que coloniza hojas y espigas de cereales',
      regions: ['Castilla y León'],
      crops: ['Trigo', 'Cebada', 'Avena'],
      products: [
        { name: 'Pirimicarb', type: 'Químico', dosage: '0.75 g/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '1-2% en agua' },
        { name: 'Enemigos naturales', type: 'Control biológico', dosage: 'Conservación fauna auxiliar' }
      ]
    },
    {
      id: 18,
      name: 'Mosca de Hylemia',
      scientificName: 'Delia coarctata',
      description: 'Larva que ataca el sistema radicular de cereales',
      regions: ['Castilla y León'],
      crops: ['Trigo', 'Cebada'],
      products: [
        { name: 'Tratamiento de semillas', type: 'Químico', dosage: 'Imidacloprid semillas' },
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: 'Evitar repetición' }
      ]
    },
    {
      id: 19,
      name: 'Escarabajo de la patata',
      scientificName: 'Leptinotarsa decemlineata',
      description: 'Escarabajo rayado cuyas larvas devoran hojas de solanáceas',
      regions: ['Castilla y León'],
      crops: ['Patata', 'Berenjena', 'Tomate'],
      products: [
        { name: 'Bacillus thuringiensis var. tenebrionis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Novaluron', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Recolección manual', type: 'Físico', dosage: 'En huertos pequeños' }
      ]
    },
    {
      id: 20,
      name: 'Carpocapsa (Polilla del manzano)',
      scientificName: 'Cydia pomonella',
      description: 'Larva que perfora frutos de pepita causando galerías internas',
      regions: ['Cataluña y Aragón', 'Galicia, Asturias y Cantabria'],
      crops: ['Manzano', 'Peral', 'Membrillo'],
      products: [
        { name: 'Confusión sexual', type: 'Físico', dosage: '500 difusores/ha' },
        { name: 'Virus de la granulosis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Trampas de feromonas', type: 'Físico', dosage: 'Monitoreo y captura' }
      ]
    },
    {
      id: 21,
      name: 'Pulgón ceniciento',
      scientificName: 'Dysaphis plantaginea',
      description: 'Pulgón gris que deforma hojas y frutos del manzano',
      regions: ['Cataluña y Aragón'],
      crops: ['Manzano'],
      products: [
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' },
        { name: 'Pirimicarb', type: 'Químico', dosage: '0.75 g/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' }
      ]
    },
    {
      id: 22,
      name: 'Oruga del maíz',
      scientificName: 'Ostrinia nubilalis',
      description: 'Oruga que perfora tallos de maíz debilitando la planta',
      regions: ['Cataluña y Aragón'],
      crops: ['Maíz'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Trichogramma brassicae', type: 'Control biológico', dosage: 'Sueltas periódicas' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' }
      ]
    },
    {
      id: 23,
      name: 'Mosca de la cereza',
      scientificName: 'Rhagoletis cerasi',
      description: 'Mosca que pone huevos en cerezas en maduración, larvas estropean el fruto',
      regions: ['Cataluña y Aragón'],
      crops: ['Cerezo'],
      products: [
        { name: 'Trampas amarillas con atrayente', type: 'Físico', dosage: '8-12 trampas/árbol' },
        { name: 'Spinosad (cebo)', type: 'Biológico', dosage: 'Aplicación localizada' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' }
      ]
    },
    {
      id: 24,
      name: 'Avispilla del castaño',
      scientificName: 'Dryocosmus kuriphilus',
      description: 'Forma agallas en brotes jóvenes reduciendo producción de castañas',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Castaño'],
      products: [
        { name: 'Torymus sinensis', type: 'Control biológico', dosage: 'Suelta de parasitoides' },
        { name: 'Poda de agallas', type: 'Cultural', dosage: 'Eliminación en invierno' }
      ]
    },
    {
      id: 25,
      name: 'Picudo negro del plátano',
      scientificName: 'Cosmopolites sordidus',
      description: 'Gorgojo negro cuyas larvas perforan el rizoma del plátano',
      regions: ['Canarias y Baleares'],
      crops: ['Plátano'],
      products: [
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '3 g/L' },
        { name: 'Trampas con feromona', type: 'Físico', dosage: '20 trampas/ha' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Limpieza cultural', type: 'Cultural', dosage: 'Eliminar restos vegetales' }
      ]
    },
    {
      id: 26,
      name: 'Araña roja',
      scientificName: 'Tetranychus urticae',
      description: 'Ácaro que provoca decoloración amarillenta, manchas y caída de hojas',
      regions: ['Andalucía'],
      crops: ['Tomate', 'Fresa', 'Pepino', 'Judía', 'Algodón'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Azufre mojable', type: 'Ecológico', dosage: '3-5 g/L' },
        { name: 'Phytoseiulus persimilis', type: 'Control biológico', dosage: '5-10 ind/m²' },
        { name: 'Aceite de parafina', type: 'Ecológico', dosage: '1.5% en agua' }
      ]
    },
    {
      id: 27,
      name: 'Helicoverpa armigera (Rosquilla del tomate)',
      scientificName: 'Helicoverpa armigera',
      description: 'Oruga muy polífaga que daña frutos, flores y hojas',
      regions: ['Andalucía', 'Cataluña y Aragón', 'Galicia, Asturias y Cantabria', 'Canarias y Baleares'],
      crops: ['Tomate', 'Pimiento', 'Algodón', 'Maíz'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorantraniliprol', type: 'Químico', dosage: '0.3 ml/L' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '1 trampa/1000m²' }
      ]
    },
    {
      id: 28,
      name: 'Chinche verde',
      scientificName: 'Nezara viridula',
      description: 'Chinche que succiona savia y deforma frutos y semillas',
      regions: ['Andalucía'],
      crops: ['Legumbres', 'Tomate', 'Pimiento', 'Hortalizas'],
      products: [
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Recolección manual', type: 'Físico', dosage: 'En infestaciones bajas' }
      ]
    },
    {
      id: 29,
      name: 'Prays del olivo',
      scientificName: 'Prays oleae',
      description: 'Polilla que ataca flores, frutos y hojas del olivo',
      regions: ['Andalucía'],
      crops: ['Olivar'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Confusión sexual', type: 'Físico', dosage: '400-500 difusores/ha' },
        { name: 'Dimetoato', type: 'Químico', dosage: '1.5 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo' }
      ]
    },
    {
      id: 30,
      name: 'Barrenadores del almendro',
      scientificName: 'Cydia splendana / Euzophera bigella',
      description: 'Larvas que perforan almendras y ramas',
      regions: ['Andalucía'],
      crops: ['Almendro', 'Nogal'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Poda sanitaria', type: 'Cultural', dosage: 'Eliminación de ramas afectadas' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo y captura masiva' }
      ]
    },
    {
      id: 31,
      name: 'Barrenador del ciprés',
      scientificName: 'Phloeosinus armatus',
      description: 'Escarabajo que perfora corteza de coníferas ornamentales',
      regions: ['Andalucía'],
      crops: ['Ciprés', 'Plantaciones ornamentales'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Poda de ramas secas', type: 'Cultural', dosage: 'Eliminación inmediata' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 32,
      name: 'Ácaro del tomate',
      scientificName: 'Tetranychus evansi',
      description: 'Ácaro específico de solanáceas, más resistente que araña roja',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Tomate', 'Berenjena'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Phytoseiulus longipes', type: 'Control biológico', dosage: '5-10 ind/m²' },
        { name: 'Azufre mojable', type: 'Ecológico', dosage: '4-5 g/L' }
      ]
    },
    {
      id: 33,
      name: 'Psila del peral',
      scientificName: 'Cacopsylla pyri',
      description: 'Insecto chupador que produce melaza y debilita el árbol',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Peral'],
      products: [
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' },
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' }
      ]
    },
    {
      id: 34,
      name: 'Barrenador del arroz',
      scientificName: 'Chilo suppressalis',
      description: 'Oruga que perfora tallos de arroz causando corazón muerto',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Arroz'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Trichogramma japonicum', type: 'Control biológico', dosage: 'Sueltas periódicas' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' }
      ]
    },
    {
      id: 35,
      name: 'Mosca blanca de la col',
      scientificName: 'Aleyrodes proletella',
      description: 'Mosca blanca específica de crucíferas',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Coles', 'Brócoli', 'Coliflor', 'Brassicas'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' },
        { name: 'Encarsia formosa', type: 'Control biológico', dosage: '3-5 ind/m²' }
      ]
    },
    {
      id: 36,
      name: 'Avispa del almendro',
      scientificName: 'Eurytoma amygdali',
      description: 'Larva que se alimenta del interior de la almendra',
      regions: ['Castilla-La Mancha'],
      crops: ['Almendro'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L en floración' },
        { name: 'Recolección de frutos momificados', type: 'Cultural', dosage: 'Eliminar antes de floración' },
        { name: 'Trampas cromáticas', type: 'Físico', dosage: 'Monitoreo' }
      ]
    },
    {
      id: 37,
      name: 'Cochinilla del olivo',
      scientificName: 'Aspidiotus nerii',
      description: 'Cochinilla que forma escudos en ramas y hojas',
      regions: ['Castilla-La Mancha'],
      crops: ['Olivo', 'Cítricos'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aphytis spp.', type: 'Control biológico', dosage: 'Suelta de parasitoides' }
      ]
    },
    {
      id: 38,
      name: 'Zabrus (Gusano gris de cereales)',
      scientificName: 'Zabrus tenebrioides',
      description: 'Larva y adulto devoran hojas y espigas de cereales',
      regions: ['Castilla-La Mancha'],
      crops: ['Trigo', 'Cebada', 'Centeno'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Laboreo profundo', type: 'Cultural', dosage: 'Tras cosecha' },
        { name: 'Trampas de luz', type: 'Físico', dosage: 'Captura de adultos' }
      ]
    },
    {
      id: 39,
      name: 'Polilla del trigo almacenado',
      scientificName: 'Sitotroga cerealella',
      description: 'Polilla que ataca granos de cereal en almacenes',
      regions: ['Castilla-La Mancha'],
      crops: ['Trigo', 'Maíz', 'Arroz almacenado'],
      products: [
        { name: 'Fosfina', type: 'Químico', dosage: 'Fumigación profesional' },
        { name: 'Trichogramma evanescens', type: 'Control biológico', dosage: 'Sueltas en almacén' },
        { name: 'Control de temperatura', type: 'Físico', dosage: '<15°C' }
      ]
    },
    {
      id: 40,
      name: 'Gusano de las raíces',
      scientificName: 'Tanymecus dilaticollis',
      description: 'Larva que devora raíces de cultivos industriales',
      regions: ['Castilla-La Mancha'],
      crops: ['Remolacha', 'Girasol', 'Maíz'],
      products: [
        { name: 'Imidacloprid en semilla', type: 'Químico', dosage: 'Tratamiento de semilla' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '3 g/L al suelo' },
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: 'Evitar repetición' }
      ]
    },
    {
      id: 41,
      name: 'Gorgojo de la alfalfa',
      scientificName: 'Hypera postica',
      description: 'Larva verde que esqueletiza hojas de alfalfa',
      regions: ['Castilla-La Mancha'],
      crops: ['Alfalfa'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Bathyplectes curculionis', type: 'Control biológico', dosage: 'Parasitoide natural' },
        { name: 'Corte anticipado', type: 'Cultural', dosage: 'Adelantar siega' }
      ]
    },
    {
      id: 42,
      name: 'Mosca del trigo',
      scientificName: 'Oscinella frit',
      description: 'Larva que ataca el tallo principal causando ahijamiento anormal',
      regions: ['Castilla y León'],
      crops: ['Trigo', 'Cebada', 'Maíz'],
      products: [
        { name: 'Imidacloprid en semilla', type: 'Químico', dosage: 'Tratamiento preventivo' },
        { name: 'Siembra tardía', type: 'Cultural', dosage: 'Evitar vuelo de adultos' },
        { name: 'Variedades resistentes', type: 'Cultural', dosage: 'Selección varietal' }
      ]
    },
    {
      id: 43,
      name: 'Gusano negro de cereales',
      scientificName: 'Blapstinus punctulatus',
      description: 'Escarabajo negro que corta plántulas a ras de suelo',
      regions: ['Castilla y León'],
      crops: ['Cereales', 'Remolacha'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Cebos envenenados', type: 'Químico', dosage: 'Aplicación localizada' },
        { name: 'Laboreo previo', type: 'Cultural', dosage: 'Exponer larvas' }
      ]
    },
    {
      id: 44,
      name: 'Gusano de alambre',
      scientificName: 'Agriotes lineatus',
      description: 'Larva dura que perfora tubérculos y raíces',
      regions: ['Castilla y León'],
      crops: ['Patata', 'Remolacha', 'Maíz'],
      products: [
        { name: 'Clorpirifos al suelo', type: 'Químico', dosage: '20 kg/ha' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '4-6 trampas/ha' },
        { name: 'Rotación con leguminosas', type: 'Cultural', dosage: 'Romper ciclo' }
      ]
    },
    {
      id: 45,
      name: 'Polilla de los granos',
      scientificName: 'Ephestia kuehniella',
      description: 'Polilla gris que infesta harinas y granos almacenados',
      regions: ['Castilla y León'],
      crops: ['Cereales almacenados', 'Harinas'],
      products: [
        { name: 'Fosfina', type: 'Químico', dosage: 'Fumigación profesional' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '1 trampa/100m²' },
        { name: 'Trichogramma evanescens', type: 'Control biológico', dosage: 'Sueltas periódicas' }
      ]
    },
    {
      id: 46,
      name: 'Polilla oriental del melocotonero',
      scientificName: 'Grapholita molesta',
      description: 'Larva que perfora brotes y frutos de frutales de hueso',
      regions: ['Cataluña y Aragón'],
      crops: ['Melocotonero', 'Nectarina', 'Albaricoquero'],
      products: [
        { name: 'Confusión sexual', type: 'Físico', dosage: '500 difusores/ha' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' }
      ]
    },
    {
      id: 47,
      name: 'Mosca del peral',
      scientificName: 'Hoplocampa brevis',
      description: 'Larva que perfora frutos jóvenes provocando su caída',
      regions: ['Cataluña y Aragón'],
      crops: ['Peral'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L en floración' },
        { name: 'Trampas blancas', type: 'Físico', dosage: 'Monitoreo de adultos' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' }
      ]
    },
    {
      id: 48,
      name: 'Gorgojo del manzano',
      scientificName: 'Phyllobius oblongus',
      description: 'Escarabajo verde que devora hojas y yemas',
      regions: ['Cataluña y Aragón'],
      crops: ['Manzano', 'Peral'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Recolección manual', type: 'Físico', dosage: 'Sacudir ramas al amanecer' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2 g/L' }
      ]
    },
    {
      id: 49,
      name: 'Pulgón verde del manzano',
      scientificName: 'Aphis pomi',
      description: 'Pulgón verde que enrolla hojas y deforma frutos',
      regions: ['Cataluña y Aragón'],
      crops: ['Manzano'],
      products: [
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' },
        { name: 'Pirimicarb', type: 'Químico', dosage: '0.75 g/L' },
        { name: 'Aphidius colemani', type: 'Control biológico', dosage: '1-2 ind/m²' }
      ]
    },
    {
      id: 50,
      name: 'Metcalfa',
      scientificName: 'Metcalfa pruinosa',
      description: 'Cicadélido invasor polífago que produce melaza abundante',
      regions: ['Cataluña y Aragón'],
      crops: ['Frutales', 'Vid', 'Ornamentales'],
      products: [
        { name: 'Neodryinus typhlocybae', type: 'Control biológico', dosage: 'Parasitoide específico' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 51,
      name: 'Barrenador del melocotonero',
      scientificName: 'Anarsia lineatella',
      description: 'Larva que perfora brotes tiernos y frutos',
      regions: ['Cataluña y Aragón'],
      crops: ['Melocotonero', 'Albaricoquero', 'Ciruelo'],
      products: [
        { name: 'Confusión sexual', type: 'Físico', dosage: '400-500 difusores/ha' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' }
      ]
    },
    {
      id: 52,
      name: 'Gorgojo del castaño',
      scientificName: 'Curculio elephas',
      description: 'Gorgojo con trompa larga que perfora castañas',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Castaño'],
      products: [
        { name: 'Tratamiento térmico', type: 'Físico', dosage: '45°C por 2 horas' },
        { name: 'Recolección temprana', type: 'Cultural', dosage: 'Cosechar al suelo' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' }
      ]
    },
    {
      id: 53,
      name: 'Taladro del manzano',
      scientificName: 'Cossus cossus',
      description: 'Larva grande que perfora galerías en troncos y ramas',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Manzano', 'Peral', 'Sauce'],
      products: [
        { name: 'Inyección en galerías', type: 'Químico', dosage: 'Clorpirifos directo' },
        { name: 'Poda de ramas afectadas', type: 'Cultural', dosage: 'Eliminar y quemar' },
        { name: 'Alambre flexible', type: 'Físico', dosage: 'Matar larvas en galería' }
      ]
    },
    {
      id: 54,
      name: 'Defoliador del roble',
      scientificName: 'Tortrix viridana',
      description: 'Oruga verde que devora hojas de Quercus',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Roble', 'Encina', 'Alcornoque'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Control biológico natural', type: 'Cultural', dosage: 'Fomentar aves insectívoras' },
        { name: 'Diflubenzuron', type: 'Químico', dosage: '0.5 ml/L' }
      ]
    },
    {
      id: 55,
      name: 'Minador del manzano',
      scientificName: 'Phyllonorycter blancardella',
      description: 'Larva diminuta que mina hojas formando ampollas',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Manzano'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aceite de parafina', type: 'Ecológico', dosage: '1.5% en agua' },
        { name: 'Conservar enemigos naturales', type: 'Cultural', dosage: 'Control biológico natural' }
      ]
    },
    {
      id: 56,
      name: 'Cochinilla de la vid',
      scientificName: 'Planococcus ficus',
      description: 'Cochinilla algodonosa que ataca racimos de uva',
      regions: ['Canarias y Baleares'],
      crops: ['Viña'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '5-10 ind/cepa' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' }
      ]
    },
    {
      id: 57,
      name: 'Cochinilla del nopal',
      scientificName: 'Dactylopius opuntiae',
      description: 'Cochinilla que coloniza tuneras produciendo cera blanca',
      regions: ['Canarias y Baleares'],
      crops: ['Nopal', 'Tunera'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5%' },
        { name: 'Recolección manual', type: 'Físico', dosage: 'Eliminar pencas afectadas' }
      ]
    },
    {
      id: 58,
      name: 'Mosca blanca espiral',
      scientificName: 'Aleurodicus dispersus',
      description: 'Mosca blanca con patrón espiral de cera, muy polífaga',
      regions: ['Canarias y Baleares'],
      crops: ['Aguacate', 'Cítricos', 'Ornamentales'],
      products: [
        { name: 'Encarsia guadeloupae', type: 'Control biológico', dosage: 'Parasitoide específico' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 59,
      name: 'Spodoptera exigua (Rosquilla verde)',
      scientificName: 'Spodoptera exigua',
      description: 'Oruga verde muy polífaga que devora hojas, flores y frutos',
      regions: ['Andalucía', 'Canarias y Baleares'],
      crops: ['Tomate', 'Pimiento', 'Lechuga', 'Judía', 'Maíz', 'Algodón'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '1 trampa/1000m²' }
      ]
    },
    {
      id: 60,
      name: 'Rosquilla del algodón',
      scientificName: 'Spodoptera littoralis',
      description: 'Oruga muy polífaga que causa defoliación severa',
      regions: ['Andalucía'],
      crops: ['Tomate', 'Berenjena', 'Algodón', 'Pimiento'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorantraniliprol', type: 'Químico', dosage: '0.3 ml/L' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '1 trampa/1000m²' }
      ]
    },
    {
      id: 61,
      name: 'Pulgón del cítrico',
      scientificName: 'Aphis spiraecola',
      description: 'Pulgón que coloniza brotes tiernos de cítricos enrollando hojas',
      regions: ['Andalucía'],
      crops: ['Cítricos jóvenes', 'Brotes tiernos'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '1-2% en agua' },
        { name: 'Pirimicarb', type: 'Químico', dosage: '0.75 g/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' },
        { name: 'Aphidius colemani', type: 'Control biológico', dosage: '1-2 ind/m²' }
      ]
    },
    {
      id: 62,
      name: 'Psila del ciruelo',
      scientificName: 'Cacopsylla pruni',
      description: 'Vector de fitoplasmas que causan enfermedades en frutales de hueso',
      regions: ['Andalucía'],
      crops: ['Almendro', 'Ciruelo'],
      products: [
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' },
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' }
      ]
    },
    {
      id: 63,
      name: 'Taladro del frutal',
      scientificName: 'Zeuzera pyrina',
      description: 'Larva grande que perfora galerías en troncos y ramas',
      regions: ['Andalucía'],
      crops: ['Olivar joven', 'Almendro', 'Manzano', 'Peral'],
      products: [
        { name: 'Inyección en galerías', type: 'Químico', dosage: 'Clorpirifos directo' },
        { name: 'Poda de ramas afectadas', type: 'Cultural', dosage: 'Eliminar y quemar' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Captura masiva machos' }
      ]
    },
    {
      id: 64,
      name: 'Escarabajo perforador del olivo',
      scientificName: 'Hylesinus oleiperda',
      description: 'Escarabajo que perfora ramas de olivo debilitado',
      regions: ['Andalucía', 'Castilla-La Mancha'],
      crops: ['Olivar'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Poda sanitaria', type: 'Cultural', dosage: 'Eliminar ramas secas' },
        { name: 'Quema de restos', type: 'Cultural', dosage: 'Destruir material afectado' }
      ]
    },
    {
      id: 65,
      name: 'Cochinilla blanca del melocotonero',
      scientificName: 'Pseudaulacaspis pentagona',
      description: 'Cochinilla que forma costras blancas en ramas y frutos',
      regions: ['Andalucía'],
      crops: ['Melocotonero', 'Albaricoquero', 'Ciruelo'],
      products: [
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Encarsia berlesei', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 66,
      name: 'Ácaro rojo común',
      scientificName: 'Tetranychus cinnabarinus',
      description: 'Ácaro rojo que causa decoloración y caída prematura de hojas',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Pimiento', 'Tomate', 'Berenjena'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Azufre mojable', type: 'Ecológico', dosage: '3-5 g/L' },
        { name: 'Phytoseiulus persimilis', type: 'Control biológico', dosage: '5-10 ind/m²' },
        { name: 'Aceite de parafina', type: 'Ecológico', dosage: '1.5% en agua' }
      ]
    },
    {
      id: 67,
      name: 'Cochinilla gris del naranjo',
      scientificName: 'Parlatoria pergandii',
      description: 'Cochinilla que forma escudos grises en frutos y hojas',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Aphytis lepidosaphes', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 68,
      name: 'Cochinilla parlatoria',
      scientificName: 'Chrysomphalus aonidum',
      description: 'Cochinilla circular que infesta hojas y frutos de cítricos',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aphytis holoxanthus', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 69,
      name: 'Vector del bois noir',
      scientificName: 'Hyalestes obsoletus',
      description: 'Cicadélido vector de fitoplasma que causa decaimiento de la vid',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Viñedos'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Control de malezas', type: 'Cultural', dosage: 'Eliminar ortigas y convolvulus' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' }
      ]
    },
    {
      id: 70,
      name: 'Ácaro de la deformación del limón',
      scientificName: 'Aceria sheldoni',
      description: 'Ácaro microscópico que deforma flores y frutos del limón',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Limonero'],
      products: [
        { name: 'Azufre mojable', type: 'Ecológico', dosage: '4-5 g/L' },
        { name: 'Abamectina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Aceite de parafina', type: 'Ecológico', dosage: '1.5% en agua' }
      ]
    },
    {
      id: 71,
      name: 'Tordeuse del manzano',
      scientificName: 'Adoxophyes orana',
      description: 'Oruga que enrolla hojas y daña frutos',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Manzano', 'Caqui', 'Peral'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo y captura' }
      ]
    },
    {
      id: 72,
      name: 'Barrenillo del olivo',
      scientificName: 'Euzophera pinguis',
      description: 'Larva que perfora troncos y ramas principales',
      regions: ['Castilla-La Mancha'],
      crops: ['Olivar'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L en tronco' },
        { name: 'Poda sanitaria', type: 'Cultural', dosage: 'Eliminar partes afectadas' },
        { name: 'Encalado de troncos', type: 'Cultural', dosage: 'Repelente físico' }
      ]
    },
    {
      id: 73,
      name: 'Gusano cabezudo',
      scientificName: 'Capnodis tenebrionis',
      description: 'Escarabajo negro cuyas larvas devoran raíces de frutales',
      regions: ['Castilla-La Mancha'],
      crops: ['Almendro', 'Melocotonero', 'Cerezo', 'Albaricoquero'],
      products: [
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '3 g/L al suelo' },
        { name: 'Recolección manual adultos', type: 'Físico', dosage: 'Sacudir árboles' },
        { name: 'Clorpirifos al cuello', type: 'Químico', dosage: '2 ml/L' }
      ]
    },
    {
      id: 74,
      name: 'Barrenador secundario del olivo',
      scientificName: 'Hylesinus varius',
      description: 'Escarabajo que ataca olivos debilitados',
      regions: ['Castilla-La Mancha'],
      crops: ['Olivar'],
      products: [
        { name: 'Poda de ramas secas', type: 'Cultural', dosage: 'Eliminar material afectado' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Mejora del estado fitosanitario', type: 'Cultural', dosage: 'Riego y nutrición' }
      ]
    },
    {
      id: 75,
      name: 'Gorgojo del guisante',
      scientificName: 'Sitona lineatus',
      description: 'Escarabajo que mordisquea hojas de leguminosas',
      regions: ['Castilla-La Mancha'],
      crops: ['Guisante', 'Haba', 'Lenteja'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2 g/L' },
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: 'Evitar repetición' }
      ]
    },
    {
      id: 76,
      name: 'Pulguilla del maíz',
      scientificName: 'Chaetocnema pulicaria',
      description: 'Escarabajo diminuto que perfora hojas de plántulas',
      regions: ['Castilla y León'],
      crops: ['Maíz'],
      products: [
        { name: 'Imidacloprid en semilla', type: 'Químico', dosage: 'Tratamiento preventivo' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Siembra temprana', type: 'Cultural', dosage: 'Evitar periodo crítico' }
      ]
    },
    {
      id: 77,
      name: 'Escarabajo de la avena',
      scientificName: 'Lema melanopa',
      description: 'Escarabajo y larva que devoran hojas de cereales',
      regions: ['Castilla y León'],
      crops: ['Avena', 'Trigo', 'Cebada'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: 'Cambiar cultivo' }
      ]
    },
    {
      id: 78,
      name: 'Rosquilla gris',
      scientificName: 'Agrotis segetum',
      description: 'Oruga gris que corta plántulas a ras de suelo por la noche',
      regions: ['Castilla y León'],
      crops: ['Cereales', 'Remolacha', 'Patata', 'Hortalizas'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Cebos envenenados', type: 'Químico', dosage: 'Aplicación nocturna' },
        { name: 'Laboreo profundo', type: 'Cultural', dosage: 'Exponer pupas' }
      ]
    },
    {
      id: 79,
      name: 'Pulguilla de las coles',
      scientificName: 'Phyllotreta cruciferae',
      description: 'Escarabajo diminuto que perfora hojas de crucíferas',
      regions: ['Castilla y León'],
      crops: ['Coles', 'Brócoli', 'Coliflor', 'Rábano'],
      products: [
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Mallas anti-insectos', type: 'Físico', dosage: 'Protección de semilleros' }
      ]
    },
    {
      id: 80,
      name: 'Mosca de la col',
      scientificName: 'Delia radicum',
      description: 'Larva que ataca raíces de crucíferas',
      regions: ['Castilla y León'],
      crops: ['Col', 'Coliflor', 'Brócoli', 'Nabo'],
      products: [
        { name: 'Clorpirifos al suelo', type: 'Químico', dosage: '20 kg/ha' },
        { name: 'Discos protectores', type: 'Físico', dosage: 'Alrededor del cuello' },
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: '3-4 años' }
      ]
    },
    {
      id: 81,
      name: 'Pulgón lanígero del manzano',
      scientificName: 'Eriosoma lanigerum',
      description: 'Pulgón cubierto de cera blanca que forma nódulos en ramas',
      regions: ['Cataluña y Aragón'],
      crops: ['Manzano'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aphelinus mali', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 82,
      name: 'Pulgón harinoso del ciruelo',
      scientificName: 'Hyalopterus pruni',
      description: 'Pulgón verde cubierto de cera que coloniza brotes',
      regions: ['Cataluña y Aragón'],
      crops: ['Ciruelo', 'Melocotonero', 'Albaricoquero'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Pirimicarb', type: 'Químico', dosage: '0.75 g/L' },
        { name: 'Aphidius colemani', type: 'Control biológico', dosage: '1-2 ind/m²' }
      ]
    },
    {
      id: 83,
      name: 'Piojo de San José',
      scientificName: 'Quadraspidiotus perniciosus',
      description: 'Cochinilla muy dañina que forma costras en corteza y frutos',
      regions: ['Cataluña y Aragón'],
      crops: ['Manzano', 'Peral', 'Melocotonero', 'Ciruelo'],
      products: [
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Encarsia perniciosi', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 84,
      name: 'Polilla de la uva',
      scientificName: 'Cryptoblabes gnidiella',
      description: 'Oruga que ataca racimos de uva y granadas',
      regions: ['Cataluña y Aragón'],
      crops: ['Vid', 'Granado'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo' }
      ]
    },
    {
      id: 85,
      name: 'Defoliadora de la alfalfa',
      scientificName: 'Gonioctena fornicata',
      description: 'Escarabajo que devora hojas de alfalfa',
      regions: ['Cataluña y Aragón'],
      crops: ['Alfalfa'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Corte anticipado', type: 'Cultural', dosage: 'Interrumpir ciclo' },
        { name: 'Enemigos naturales', type: 'Control biológico', dosage: 'Conservar fauna auxiliar' }
      ]
    },
    {
      id: 86,
      name: 'Gorgojo de la avellana',
      scientificName: 'Curculio nucum',
      description: 'Gorgojo que perfora avellanas en formación',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Avellano'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Recolección temprana', type: 'Cultural', dosage: 'Cosechar al suelo' },
        { name: 'Trampas con atrayentes', type: 'Físico', dosage: 'Captura de adultos' }
      ]
    },
    {
      id: 87,
      name: 'Barrenador del roble',
      scientificName: 'Agrilus biguttatus',
      description: 'Escarabajo metálico cuyas larvas perforan robles',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Roble', 'Encina'],
      products: [
        { name: 'Poda de ramas afectadas', type: 'Cultural', dosage: 'Eliminar y quemar' },
        { name: 'Mejorar vigor del árbol', type: 'Cultural', dosage: 'Riego y nutrición' },
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L inyección' }
      ]
    },
    {
      id: 88,
      name: 'Rosquilla negra',
      scientificName: 'Agrotis ipsilon',
      description: 'Oruga nocturna que corta plántulas a ras de suelo',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Maíz', 'Hortalizas', 'Patata'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Cebos envenenados', type: 'Químico', dosage: 'Aplicación al atardecer' },
        { name: 'Laboreo profundo', type: 'Cultural', dosage: 'Destruir crisálidas' }
      ]
    },
    {
      id: 89,
      name: 'Cochinilla del aguacate',
      scientificName: 'Coelostomidia wairoensis',
      description: 'Cochinilla que ataca frutos y hojas de aguacate',
      regions: ['Canarias y Baleares'],
      crops: ['Aguacate'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' }
      ]
    },
    {
      id: 90,
      name: 'Cochinillas tropicales',
      scientificName: 'Pseudococcidae spp.',
      description: 'Diversas cochinillas harinosas que atacan frutales tropicales',
      regions: ['Canarias y Baleares'],
      crops: ['Papaya', 'Mango', 'Aguacate'],
      products: [
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' }
      ]
    },
    {
      id: 91,
      name: 'Gusano cogollero del maíz',
      scientificName: 'Spodoptera frugiperda',
      description: 'Oruga muy destructiva que ataca el cogollo del maíz (plaga cuarentenaria)',
      regions: ['Canarias y Baleares'],
      crops: ['Maíz', 'Sorgo', 'Arroz'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Clorantraniliprol', type: 'Químico', dosage: '0.3 ml/L' },
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo intensivo' }
      ]
    },
    {
      id: 92,
      name: 'Mosca blanca secundaria',
      scientificName: 'Bemisia afer',
      description: 'Mosca blanca menos común pero presente en invernaderos',
      regions: ['Canarias y Baleares'],
      crops: ['Tomate', 'Pimiento'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Spiromesifen', type: 'Químico', dosage: '1 ml/L' },
        { name: 'Eretmocerus mundus', type: 'Control biológico', dosage: '5 ind/m²' }
      ]
    },
    {
      id: 93,
      name: 'Mosca blanca del tomate',
      scientificName: 'Aleurotrachelus trachoides',
      description: 'Mosca blanca específica del tomate presente en islas orientales',
      regions: ['Canarias y Baleares'],
      crops: ['Tomate'],
      products: [
        { name: 'Spiromesifen', type: 'Químico', dosage: '1 ml/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2 g/L' }
      ]
    },
    {
      id: 94,
      name: 'Cigarrillas verdes',
      scientificName: 'Empoasca spp.',
      description: 'Cicadélidos que succionan savia causando clorosis y enrollamiento de hojas',
      regions: ['Andalucía', 'Murcia y C. Valenciana'],
      crops: ['Hortalizas', 'Frutales', 'Judía', 'Remolacha'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 95,
      name: 'Gorgojo del olivo',
      scientificName: 'Otiorhynchus cribricollis',
      description: 'Gorgojo que devora hojas y sus larvas atacan raíces',
      regions: ['Andalucía'],
      crops: ['Olivar', 'Frutales'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '3 g/L al suelo' },
        { name: 'Nematodos entomopatógenos', type: 'Biológico', dosage: '500.000 ind/m²' }
      ]
    },
    {
      id: 96,
      name: 'Chicharra espumadora',
      scientificName: 'Philaenus spumarius',
      description: 'Vector de Xylella fastidiosa, forma espuma en tallos',
      regions: ['Andalucía'],
      crops: ['Olivar', 'Almendro', 'Vid', 'Cítricos'],
      products: [
        { name: 'Control de vegetación espontánea', type: 'Cultural', dosage: 'Eliminar hospedantes alternativos' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 97,
      name: 'Escarabajo del tabaco',
      scientificName: 'Lasioderma serricorne',
      description: 'Escarabajo que infesta granos, tabaco y hierbas almacenadas',
      regions: ['Andalucía'],
      crops: ['Cereales almacenados', 'Tabaco', 'Hierbas aromáticas'],
      products: [
        { name: 'Fosfina', type: 'Químico', dosage: 'Fumigación profesional' },
        { name: 'Control de temperatura', type: 'Físico', dosage: '<18°C' },
        { name: 'Tierra de diatomeas', type: 'Ecológico', dosage: '1 kg/tonelada' }
      ]
    },
    {
      id: 98,
      name: 'Picudo del boniato',
      scientificName: 'Cylas formicarius elegantulus',
      description: 'Gorgojo que perfora tubérculos de batata (vigilancia fitosanitaria)',
      regions: ['Andalucía'],
      crops: ['Boniato', 'Batata'],
      products: [
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: 'Evitar repetición' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo y detección' },
        { name: 'Inspección de material vegetal', type: 'Cultural', dosage: 'Control preventivo' }
      ]
    },
    {
      id: 99,
      name: 'Chinches fitófagas',
      scientificName: 'Heteroptera spp.',
      description: 'Diversas especies de chinches que succionan savia y deforman frutos',
      regions: ['Andalucía'],
      crops: ['Pimiento', 'Berenjena', 'Tomate'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Recolección manual', type: 'Físico', dosage: 'En infestaciones bajas' }
      ]
    },
    {
      id: 100,
      name: 'Psílido africano de los cítricos',
      scientificName: 'Trioza erytreae',
      description: 'Vector del HLB (Huanglongbing), enfermedad grave de cítricos',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5%' },
        { name: 'Vigilancia fitosanitaria', type: 'Cultural', dosage: 'Monitoreo intensivo' }
      ]
    },
    {
      id: 101,
      name: 'Trips sudafricano de los cítricos',
      scientificName: 'Scirtothrips aurantii',
      description: 'Trips que daña frutos y hojas de cítricos (en observación)',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Cítricos'],
      products: [
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas azules', type: 'Físico', dosage: '1 trampa/20m²' },
        { name: 'Orius laevigatus', type: 'Control biológico', dosage: '5 ind/m²' }
      ]
    },
    {
      id: 102,
      name: 'Cigarrilla verde de hortalizas',
      scientificName: 'Empoasca decipiens',
      description: 'Cicadélido específico de hortalizas que causa amarillamiento',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Judía', 'Tomate', 'Pimiento', 'Berenjena'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Aceite de neem', type: 'Ecológico', dosage: '5 ml/L' }
      ]
    },
    {
      id: 103,
      name: 'Trips polífago de solanáceas',
      scientificName: 'Frankliniella schultzei',
      description: 'Trips que ataca principalmente solanáceas y ornamentales',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Tomate', 'Pimiento', 'Berenjena', 'Patata'],
      products: [
        { name: 'Spinosad', type: 'Biológico', dosage: '1 ml/L' },
        { name: 'Trampas azules', type: 'Físico', dosage: '1 trampa/20m²' },
        { name: 'Orius laevigatus', type: 'Control biológico', dosage: '5 ind/m²' }
      ]
    },
    {
      id: 104,
      name: 'Polillas de almacén',
      scientificName: 'Phycita sp.',
      description: 'Polillas secundarias que infestan almendra almacenada',
      regions: ['Murcia y C. Valenciana'],
      crops: ['Almendra almacenada'],
      products: [
        { name: 'Fosfina', type: 'Químico', dosage: 'Fumigación profesional' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '1 trampa/100m²' },
        { name: 'Control de temperatura', type: 'Físico', dosage: '<15°C' }
      ]
    },
    {
      id: 105,
      name: 'Gusano blanco',
      scientificName: 'Anomala dubia',
      description: 'Larva de coleóptero que devora raíces de cultivos',
      regions: ['Castilla-La Mancha'],
      crops: ['Cereal', 'Remolacha', 'Viñedo', 'Hortalizas'],
      products: [
        { name: 'Clorpirifos al suelo', type: 'Químico', dosage: '20 kg/ha' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '3 g/L al suelo' },
        { name: 'Laboreo profundo', type: 'Cultural', dosage: 'Destruir larvas y pupas' }
      ]
    },
    {
      id: 106,
      name: 'Rosquilla grande',
      scientificName: 'Noctua pronuba',
      description: 'Oruga grande que corta plántulas a ras de suelo durante la noche',
      regions: ['Castilla-La Mancha'],
      crops: ['Cereales', 'Remolacha', 'Hortalizas', 'Viñedo joven'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Cebos envenenados', type: 'Químico', dosage: 'Aplicación al atardecer' },
        { name: 'Laboreo profundo', type: 'Cultural', dosage: 'Exponer crisálidas' }
      ]
    },
    {
      id: 107,
      name: 'Pulguilla de las crucíferas',
      scientificName: 'Phyllotreta nemorum',
      description: 'Escarabajo saltador que perfora hojas de crucíferas',
      regions: ['Castilla-La Mancha'],
      crops: ['Colza', 'Col', 'Coliflor', 'Nabo', 'Rábano'],
      products: [
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Mallas anti-insectos', type: 'Físico', dosage: 'Protección de semilleros' }
      ]
    },
    {
      id: 108,
      name: 'Chinche del trigo',
      scientificName: 'Aelia rostrata',
      description: 'Chinche que succiona granos de trigo afectando su calidad panadera',
      regions: ['Castilla-La Mancha'],
      crops: ['Trigo', 'Cebada'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L en espigado' },
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Control de márgenes', type: 'Cultural', dosage: 'Eliminar malezas hospedantes' }
      ]
    },
    {
      id: 109,
      name: 'Chinche de los cereales',
      scientificName: 'Eurygaster maura',
      description: 'Chinche grande que daña granos provocando pérdida de calidad',
      regions: ['Castilla-La Mancha'],
      crops: ['Trigo', 'Cebada', 'Avena'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Siembra tardía', type: 'Cultural', dosage: 'Evitar vuelo primaveral' }
      ]
    },
    {
      id: 110,
      name: 'Gorgojo del trébol',
      scientificName: 'Hypera nigrirostris',
      description: 'Gorgojo que ataca trébol y otras leguminosas forrajeras',
      regions: ['Castilla-La Mancha'],
      crops: ['Trébol', 'Alfalfa', 'Veza'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Beauveria bassiana', type: 'Biológico', dosage: '2 g/L' },
        { name: 'Corte anticipado', type: 'Cultural', dosage: 'Interrumpir desarrollo larval' }
      ]
    },
    {
      id: 111,
      name: 'Escarabajo del cereal',
      scientificName: 'Oulema melanopus',
      description: 'Escarabajo que esqueletiza hojas de cereales',
      regions: ['Castilla-La Mancha'],
      crops: ['Trigo', 'Cebada', 'Avena', 'Centeno'],
      products: [
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Piretrinas naturales', type: 'Ecológico', dosage: '2 ml/L' },
        { name: 'Enemigos naturales', type: 'Control biológico', dosage: 'Conservar fauna auxiliar' }
      ]
    },
    {
      id: 112,
      name: 'Mosca de la colza',
      scientificName: 'Delia floralis',
      description: 'Larva que ataca raíces de colza en suelos fríos',
      regions: ['Castilla y León'],
      crops: ['Colza'],
      products: [
        { name: 'Imidacloprid en semilla', type: 'Químico', dosage: 'Tratamiento preventivo' },
        { name: 'Clorpirifos al suelo', type: 'Químico', dosage: '20 kg/ha' },
        { name: 'Siembra en fecha óptima', type: 'Cultural', dosage: 'Evitar periodo crítico' }
      ]
    },
    {
      id: 113,
      name: 'Alacrán cebollero',
      scientificName: 'Gryllotalpa gryllotalpa',
      description: 'Insecto excavador que corta raíces y plántulas bajo tierra',
      regions: ['Castilla y León'],
      crops: ['Hortalizas', 'Patata', 'Maíz', 'Cereales'],
      products: [
        { name: 'Cebos envenenados', type: 'Químico', dosage: 'Aplicación al suelo' },
        { name: 'Trampas de luz', type: 'Físico', dosage: 'Captura de adultos nocturnos' },
        { name: 'Inundación temporal', type: 'Físico', dosage: 'Ahogar galerías' }
      ]
    },
    {
      id: 114,
      name: 'Gusano de alambre oscuro',
      scientificName: 'Agriotes obscurus',
      description: 'Larva dura que perfora tubérculos y raíces',
      regions: ['Castilla y León'],
      crops: ['Patata', 'Remolacha', 'Maíz', 'Zanahoria'],
      products: [
        { name: 'Clorpirifos al suelo', type: 'Químico', dosage: '20 kg/ha' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: '4-6 trampas/ha' },
        { name: 'Rotación con leguminosas', type: 'Cultural', dosage: 'Romper ciclo' }
      ]
    },
    {
      id: 115,
      name: 'Gorgojo del arroz',
      scientificName: 'Sitophilus oryzae',
      description: 'Gorgojo que perfora granos de arroz y otros cereales almacenados',
      regions: ['Castilla y León'],
      crops: ['Arroz almacenado', 'Trigo', 'Maíz'],
      products: [
        { name: 'Fosfina', type: 'Químico', dosage: 'Fumigación profesional' },
        { name: 'Tierra de diatomeas', type: 'Ecológico', dosage: '1 kg/tonelada' },
        { name: 'Control de temperatura', type: 'Físico', dosage: '<15°C' }
      ]
    },
    {
      id: 116,
      name: 'Oruga defoliadora de cereales',
      scientificName: 'Crambus perlella',
      description: 'Oruga que devora hojas de cereales en primavera',
      regions: ['Castilla y León'],
      crops: ['Trigo', 'Cebada', 'Avena'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Control de rastrojos', type: 'Cultural', dosage: 'Eliminar residuos' }
      ]
    },
    {
      id: 117,
      name: 'Mosca de la zanahoria',
      scientificName: 'Psila rosae',
      description: 'Larva que perfora raíces de zanahoria y otras umbelíferas',
      regions: ['Castilla y León'],
      crops: ['Zanahoria', 'Apio', 'Perejil', 'Chirivía'],
      products: [
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Mallas anti-insectos', type: 'Físico', dosage: 'Protección del cultivo' },
        { name: 'Rotación de cultivos', type: 'Cultural', dosage: '3-4 años sin umbelíferas' }
      ]
    },
    {
      id: 118,
      name: 'Polilla de la ciruela',
      scientificName: 'Grapholita funebrana',
      description: 'Larva que perfora frutos de ciruelo y otros frutales de hueso',
      regions: ['Cataluña y Aragón'],
      crops: ['Ciruelo', 'Albaricoquero', 'Melocotonero'],
      products: [
        { name: 'Confusión sexual', type: 'Físico', dosage: '500 difusores/ha' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Trampas con feromonas', type: 'Físico', dosage: 'Monitoreo' }
      ]
    },
    {
      id: 119,
      name: 'Minador de la vid',
      scientificName: 'Phyllocnistis vitegenella',
      description: 'Microlepidóptero invasor reciente que mina hojas de vid',
      regions: ['Cataluña y Aragón'],
      crops: ['Viñedos'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Azadiractina', type: 'Ecológico', dosage: '3 ml/L' },
        { name: 'Control biológico natural', type: 'Cultural', dosage: 'Conservar parasitoides' }
      ]
    },
    {
      id: 120,
      name: 'Escarabajos asiáticos perforadores',
      scientificName: 'Anoplophora chinensis / A. glabripennis',
      description: 'Escarabajos exóticos muy destructivos que perforan árboles (cuarentenarios)',
      regions: ['Cataluña y Aragón'],
      crops: ['Árboles ornamentales', 'Frutales', 'Forestales'],
      products: [
        { name: 'Erradicación obligatoria', type: 'Cultural', dosage: 'Tala y destrucción' },
        { name: 'Vigilancia fitosanitaria', type: 'Cultural', dosage: 'Notificación inmediata' },
        { name: 'Inyección de insecticida', type: 'Químico', dosage: 'Tratamiento de árboles' }
      ]
    },
    {
      id: 121,
      name: 'Cochinilla H del olivo',
      scientificName: 'Saissetia oleae',
      description: 'Cochinilla hemisférica que produce melaza en olivo y cítricos',
      regions: ['Cataluña y Aragón'],
      crops: ['Olivo', 'Cítricos', 'Ornamentales'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Metaphycus helvolus', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 122,
      name: 'Psílido del puerro',
      scientificName: 'Bactericera tremblayi',
      description: 'Psílido que ataca puerro y cebolla causando deformaciones',
      regions: ['Cataluña y Aragón'],
      crops: ['Puerro', 'Cebolla', 'Ajo'],
      products: [
        { name: 'Imidacloprid', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Mallas anti-insectos', type: 'Físico', dosage: 'Protección del cultivo' }
      ]
    },
    {
      id: 123,
      name: 'Minador del tilo',
      scientificName: 'Phyllonorycter issikii',
      description: 'Microlepidóptero invasor que mina hojas de tilo',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Tilo', 'Árboles ornamentales'],
      products: [
        { name: 'Abamectina', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Control biológico natural', type: 'Cultural', dosage: 'Parasitoides nativos' },
        { name: 'Tolerancia', type: 'Cultural', dosage: 'Daño estético, no crítico' }
      ]
    },
    {
      id: 124,
      name: 'Oruga defoliadora de frutales',
      scientificName: 'Coleophora anatipennella',
      description: 'Oruga secundaria que devora hojas de frutales',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Manzano', 'Cerezo', 'Ciruelo'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Control cultural', type: 'Cultural', dosage: 'Poda y eliminación' }
      ]
    },
    {
      id: 125,
      name: 'Oruga de invierno',
      scientificName: 'Operophtera brumata',
      description: 'Oruga que aparece en invierno devorando yemas y hojas de frutales',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Manzano', 'Peral', 'Cerezo', 'Ciruelo'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Bandas adhesivas', type: 'Físico', dosage: 'En tronco para capturar hembras' },
        { name: 'Aceite mineral de invierno', type: 'Ecológico', dosage: '3-5%' }
      ]
    },
    {
      id: 126,
      name: 'Gorgojo del boj y fresa',
      scientificName: 'Otiorhynchus sulcatus',
      description: 'Gorgojo negro cuyas larvas devoran raíces de ornamentales y fresa',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Boj', 'Fresa', 'Rododendro', 'Azalea'],
      products: [
        { name: 'Nematodos entomopatógenos', type: 'Biológico', dosage: '500.000 ind/m²' },
        { name: 'Lambda cihalotrina', type: 'Químico', dosage: '0.75 ml/L' },
        { name: 'Trampas nocturnas', type: 'Físico', dosage: 'Captura manual de adultos' }
      ]
    },
    {
      id: 127,
      name: 'Lagarta peluda',
      scientificName: 'Lymantria dispar',
      description: 'Oruga muy peluda que desfolia robles y frutales en primavera',
      regions: ['Galicia, Asturias y Cantabria'],
      crops: ['Roble', 'Encina', 'Manzano', 'Peral'],
      products: [
        { name: 'Bacillus thuringiensis', type: 'Biológico', dosage: '1-2 g/L' },
        { name: 'Diflubenzuron', type: 'Químico', dosage: '0.5 ml/L' },
        { name: 'Bandas trampa', type: 'Físico', dosage: 'Captura de orugas descendentes' }
      ]
    },
    {
      id: 128,
      name: 'Cochinilla del tejo',
      scientificName: 'Aonidiella taxus',
      description: 'Cochinilla que forma escudos en ornamentales y cítricos',
      regions: ['Canarias y Baleares'],
      crops: ['Tejo', 'Cítricos', 'Ornamentales'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Aphytis spp.', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 129,
      name: 'Cochinilla del mango',
      scientificName: 'Ferrisia virgata',
      description: 'Cochinilla algodonosa que ataca frutos y hojas de mango',
      regions: ['Canarias y Baleares'],
      crops: ['Mango', 'Aguacate', 'Papaya'],
      products: [
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' }
      ]
    },
    {
      id: 130,
      name: 'Cochinilla algodonosa de cítricos',
      scientificName: 'Planococcus citri',
      description: 'Cochinilla harinosa muy común en cítricos y frutales tropicales',
      regions: ['Canarias y Baleares'],
      crops: ['Papaya', 'Plátano', 'Cítricos', 'Mango'],
      products: [
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' }
      ]
    },
    {
      id: 131,
      name: 'Cochinilla menor',
      scientificName: 'Planococcus minor',
      description: 'Cochinilla algodonosa presente en papaya y plátano',
      regions: ['Canarias y Baleares'],
      crops: ['Papaya', 'Plátano'],
      products: [
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' }
      ]
    },
    {
      id: 132,
      name: 'Cochinilla blanca del aguacate',
      scientificName: 'Pseudaulacaspis cockerelli',
      description: 'Cochinilla que forma costras blancas en ramas y frutos de aguacate',
      regions: ['Canarias y Baleares'],
      crops: ['Aguacate'],
      products: [
        { name: 'Aceite mineral de verano', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Clorpirifos', type: 'Químico', dosage: '2 ml/L' },
        { name: 'Encarsia berlesei', type: 'Control biológico', dosage: 'Parasitoide específico' }
      ]
    },
    {
      id: 133,
      name: 'Cochinilla de la piña',
      scientificName: 'Dysmicoccus brevipes',
      description: 'Cochinilla algodonosa que ataca piña tropical y otras plantas',
      regions: ['Canarias y Baleares'],
      crops: ['Piña tropical', 'Plátano', 'Ornamentales'],
      products: [
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/planta' }
      ]
    },
    {
      id: 134,
      name: 'Cochinilla verde',
      scientificName: 'Nipaecoccus viridis',
      description: 'Cochinilla verde reciente en Islas Canarias, muy polífaga',
      regions: ['Canarias y Baleares'],
      crops: ['Cítricos', 'Ornamentales', 'Frutales tropicales'],
      products: [
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Jabón potásico', type: 'Ecológico', dosage: '2% en agua' },
        { name: 'Cryptolaemus montrouzieri', type: 'Control biológico', dosage: '10-20 ind/árbol' }
      ]
    },
    {
      id: 135,
      name: 'Mosca blanca espinosa',
      scientificName: 'Aleurocanthus spiniferus',
      description: 'Mosca blanca con espinas bajo control fitosanitario',
      regions: ['Canarias y Baleares'],
      crops: ['Cítricos', 'Ornamentales'],
      products: [
        { name: 'Aceite mineral', type: 'Ecológico', dosage: '1.5-2%' },
        { name: 'Spiromesifen', type: 'Químico', dosage: '1 ml/L' },
        { name: 'Encarsia smithi', type: 'Control biológico', dosage: 'Parasitoide específico' },
        { name: 'Vigilancia fitosanitaria', type: 'Cultural', dosage: 'Control obligatorio' }
      ]
    }
  ];

  const regions = [
    'Todas',
    'Andalucía',
    'Murcia y C. Valenciana',
    'Castilla-La Mancha',
    'Castilla y León',
    'Cataluña y Aragón',
    'Galicia, Asturias y Cantabria',
    'Canarias y Baleares'
  ];

  // Filtrar plagas según búsqueda y región
  const filteredPests = pestDatabase.filter(pest => {
    const matchesSearch = 
      pest.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
      pest.scientificName.toLowerCase().includes(searchTerm.toLowerCase()) ||
      pest.crops.some(crop => crop.toLowerCase().includes(searchTerm.toLowerCase()));
    
    const matchesRegion = selectedRegion === 'Todas' || pest.regions.includes(selectedRegion);
    
    return matchesSearch && matchesRegion;
  });

  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 to-emerald-100 p-6">
      <div className="max-w-6xl mx-auto">
        {/* Header */}
        <div className="text-center mb-8">
          <div className="flex items-center justify-center gap-3 mb-4">
            <Sprout className="w-10 h-10 text-green-600" />
            <h1 className="text-4xl font-bold text-green-800">Control de Plagas Agrícolas en España</h1>
          </div>
          <p className="text-gray-600">Busca la plaga y encuentra el tratamiento adecuado por región</p>
          <p className="text-sm text-gray-500 mt-2">Base de datos con {pestDatabase.length} plagas divididas por regiones españolas</p>
        </div>

        {/* Filters Card */}
        <div className="bg-white rounded-lg shadow-lg p-6 mb-6">
          {/* Search Bar */}
          <div className="relative mb-4">
            <Search className="absolute left-3 top-3 text-gray-400 w-5 h-5" />
            <input
              type="text"
              placeholder="Buscar por nombre de plaga, nombre científico o cultivo..."
              className="w-full pl-10 pr-4 py-3 border-2 border-gray-200 rounded-lg focus:border-green-500 focus:outline-none"
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
            />
          </div>

          {/* Region Filter Toggle */}
          <button
            onClick={() => setShowFilters(!showFilters)}
            className="flex items-center gap-2 text-green-700 hover:text-green-800 font-semibold mb-3"
          >
            <Filter className="w-5 h-5" />
            {showFilters ? 'Ocultar filtros' : 'Filtrar por región'}
          </button>

          {/* Region Filter */}
          {showFilters && (
            <div className="mb-4">
              <div className="flex items-center gap-2 mb-3">
                <MapPin className="w-5 h-5 text-gray-600" />
                <label className="font-semibold text-gray-700">Región:</label>
              </div>
              <div className="grid grid-cols-2 md:grid-cols-4 gap-2">
                {regions.map(region => (
                  <button
                    key={region}
                    onClick={() => setSelectedRegion(region)}
                    className={`px-4 py-2 rounded-lg text-sm font-medium transition-all ${
                      selectedRegion === region
                        ? 'bg-green-600 text-white shadow-md'
                        : 'bg-gray-100 text-gray-700 hover:bg-gray-200'
                    }`}
                  >
                    {region}
                  </button>
                ))}
              </div>
            </div>
          )}

          {/* Active filters display */}
          {(searchTerm || selectedRegion !== 'Todas') && (
            <div className="flex flex-wrap gap-2 items-center mt-4 pt-4 border-t border-gray-200">
              <span className="text-sm text-gray-600 font-medium">Filtros activos:</span>
              {selectedRegion !== 'Todas' && (
                <span className="bg-green-100 text-green-800 px-3 py-1 rounded-full text-sm flex items-center gap-2">
                  <MapPin className="w-3 h-3" />
                  {selectedRegion}
                  <button
                    onClick={() => setSelectedRegion('Todas')}
                    className="ml-1 hover:text-green-900"
                  >
                    ×
                  </button>
                </span>
              )}
              {searchTerm && (
                <span className="bg-blue-100 text-blue-800 px-3 py-1 rounded-full text-sm flex items-center gap-2">
                  Búsqueda: "{searchTerm}"
                  <button
                    onClick={() => setSearchTerm('')}
                    className="ml-1 hover:text-blue-900"
                  >
                    ×
                  </button>
                </span>
              )}
            </div>
          )}

          {/* Results count */}
          <div className="mt-4 text-sm text-gray-600">
            {filteredPests.length} plaga{filteredPests.length !== 1 ? 's' : ''} encontrada{filteredPests.length !== 1 ? 's' : ''}
          </div>
        </div>

        {/* Results Grid */}
        {!selectedPest && filteredPests.length > 0 && (
          <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-4 mb-6">
            {filteredPests.map(pest => (
              <div
                key={pest.id}
                className="bg-white rounded-lg shadow-md p-5 cursor-pointer hover:shadow-xl transition-all border-2 border-transparent hover:border-green-500"
                onClick={() => setSelectedPest(pest)}
              >
                <div className="flex items-start gap-3">
                  <Bug className="w-8 h-8 text-red-500 flex-shrink-0 mt-1" />
                  <div className="flex-1">
                    <h3 className="font-bold text-lg text-gray-800">{pest.name}</h3>
                    <p className="text-xs text-gray-500 italic mb-2">{pest.scientificName}</p>
                    
                    {/* Regions */}
                    <div className="flex flex-wrap gap-1 mb-2">
                      {pest.regions.map((region, idx) => (
                        <span key={idx} className="text-xs bg-purple-100 text-purple-700 px-2 py-0.5 rounded flex items-center gap-1">
                          <MapPin className="w-3 h-3" />
                          {region}
                        </span>
                      ))}
                    </div>
                    
                    <p className="text-sm text-gray-600 mb-3 line-clamp-2">{pest.description}</p>
                    
                    {/* Crops */}
                    <div className="flex flex-wrap gap-1">
                      {pest.crops.slice(0, 3).map((crop, idx) => (
                        <span key={idx} className="text-xs bg-green-100 text-green-700 px-2 py-1 rounded">
                          {crop}
                        </span>
                      ))}
                      {pest.crops.length > 3 && (
                        <span className="text-xs bg-gray-100 text-gray-600 px-2 py-1 rounded">
                          +{pest.crops.length - 3} más
                        </span>
                      )}
                    </div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        )}

        {filteredPests.length === 0 && (
          <div className="text-center py-12 bg-white rounded-lg shadow-md">
            <Bug className="w-16 h-16 text-gray-300 mx-auto mb-4" />
            <p className="text-gray-500 text-lg">No se encontraron plagas con ese criterio</p>
            <p className="text-gray-400 text-sm mt-2">Intenta ajustar los filtros o cambiar la búsqueda</p>
          </div>
        )}

        {/* Selected Pest Details */}
        {selectedPest && (
          <div className="bg-white rounded-lg shadow-xl p-6 border-t-4 border-green-600">
            <button
              onClick={() => setSelectedPest(null)}
              className="text-sm text-gray-500 hover:text-gray-700 mb-4 flex items-center gap-1"
            >
              ← Volver a resultados
            </button>
            
            <div className="flex items-start gap-4 mb-6">
              <Bug className="w-12 h-12 text-red-500 flex-shrink-0" />
              <div>
                <h2 className="text-3xl font-bold text-gray-800 mb-2">{selectedPest.name}</h2>
                <p className="text-gray-500 italic text-lg">{selectedPest.scientificName}</p>
              </div>
            </div>

            <div className="mb-6">
              <h3 className="font-semibold text-gray-700 mb-2 flex items-center gap-2">
                <AlertCircle className="w-5 h-5" />
                Descripción:
              </h3>
              <p className="text-gray-600">{selectedPest.description}</p>
            </div>

            <div className="mb-6">
              <h3 className="font-semibold text-gray-700 mb-2 flex items-center gap-2">
                <MapPin className="w-5 h-5" />
                Regiones donde afecta:
              </h3>
              <div className="flex flex-wrap gap-2">
                {selectedPest.regions.map((region, idx) => (
                  <span key={idx} className="bg-purple-100 text-purple-700 px-3 py-1 rounded-full font-medium">
                    {region}
                  </span>
                ))}
              </div>
            </div>

            <div className="mb-6">
              <h3 className="font-semibold text-gray-700 mb-2">Cultivos afectados:</h3>
              <div className="flex flex-wrap gap-2">
                {selectedPest.crops.map((crop, idx) => (
                  <span key={idx} className="bg-green-100 text-green-700 px-3 py-1 rounded-full">
                    {crop}
                  </span>
                ))}
              </div>
            </div>

            <div>
              <h3 className="font-semibold text-gray-700 mb-4 text-xl">Productos recomendados:</h3>
              <div className="space-y-3">
                {selectedPest.products.map((product, idx) => (
                  <div key={idx} className="border-l-4 border-green-500 bg-gray-50 p-4 rounded">
                    <div className="flex justify-between items-start mb-2 gap-3">
                      <h4 className="font-bold text-gray-800 text-lg">{product.name}</h4>
                      <span className={`text-xs px-3 py-1 rounded-full whitespace-nowrap ${
                        product.type === 'Ecológico' ? 'bg-green-200 text-green-800' :
                        product.type === 'Biológico' || product.type === 'Control biológico' ? 'bg-emerald-200 text-emerald-800' :
                        product.type === 'Químico' ? 'bg-orange-200 text-orange-800' :
                        product.type === 'Físico' ? 'bg-blue-200 text-blue-800' :
                        'bg-purple-200 text-purple-800'
                      }`}>
                        {product.type}
                      </span>
                    </div>
                    <p className="text-gray-600">
                      <span className="font-semibold">Dosificación:</span> {product.dosage}
                    </p>
                  </div>
                ))}
              </div>
            </div>

            <div className="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-500 rounded">
              <p className="text-sm text-yellow-800">
                <strong>Nota importante:</strong> Sigue siempre las instrucciones del fabricante y respeta los plazos de seguridad. Consulta con un técnico agrícola para tratamientos específicos. Alterna productos con diferentes modos de acción para evitar resistencias.
              </p>
            </div>
          </div>
        )}
      </div>
    </div>
  );
};

export default PestControlDB;
