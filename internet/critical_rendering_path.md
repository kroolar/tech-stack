# Critical Rendering Path
Jest to sekwencja kro…ów, któ©e przeprowadza przglądark, żeby zamienić HTML, CSS i JS na pixele na ekranie.

Dostajemy HTML-a
Zaczyna parsowć HTMLA na DOM tree

Przeglądarka za każdym razem jak spotka styl, skrypt lub embedded font lub obraz

Niektóre z tych mogą blokować parsowanie i trzezba czekać aż się załadują
Następnie buduje model obiektowy CSS
 CSSOM
 
 buduje render tree
 
 
 DOM
 Incremental może być renderowany po kawałku
 Zamieniamy markup w drzewo DOM tree lub drzewo nodów.
 Im więcej tym gorzej
 
 
 CSS Object Model
 CSS blokuje , muszą się wszystkie ukończyć
 Im mniej specyficzny tym lepiej .foo jest sybzse niż .foo .barr
 
 Render TreeAnalizuje DOm CSSOM i tworzy render tree. Bierze pod uwage tylko widoczne elementy np.
 nie bierze pod uagę head, jeśłi coś ma didpaly: none też(ale pamietac ze to ejst w dom)
 
 Layout
 Określa położenie elementów na stronie, ich wysokość i szerkość oraz wzajemne położenie
 
 Paint
 Po tym jak render tree jest gotowy i adslayout to zaczyna się rysowanie pixeli na ekranie
 
 Najpierw mierzyć potem optymalizować
 
 
 DOM
 Tokenizacja i tree construction
 html first tah nody
 nested are child nodes
 atrybuty w nodach
 Im więcej ty mwiecej zajmuje tworzenie drzewa dom
 
 Img nie blokuje
 css nie blokuje
 ale script blokuje, możemy użyć async or defer
 
 Preload scanner
 Budowanie DOm tree jest głównym wątkiem ale jednoczeńsie preload scanner próbuje przeanalizować kod i zarządać plików, kóßre bęða potrzebne css ,js fonts tak a by byłu już dosteþne jak przeglądarka je napotka
 
 Trzeba dodać async lub defer, żeby upewnić się, że nic nie blokuje
 
 CSS nie blokuje parsowania HTML ale blokuje JS, ze względu na to że można coś używać
 
 
 CSSOM
 Podobne do DOM, struktura trzeba ale osobna, która konwertuje CSS rules na coś co rozumie
 Nie powinno być to coś bardzo obciążającego przewaznie zajmuje mniej niż jeden DNS lookup
 
 Other
 After CSS jest sparsowant i cSSOM utworzony
 Inne zasoby zostają pobrane, włączając. JS files
 
 JS jest zinterpretoowany, skompilowant, sparsowany i wykonany
 
 
 Budowany jest takżę AOM Accessibility object model
 Semantyczna wersja DOM, ARIA jest to potrzebne dla urządzeń pomocniczych 
 
 Interactivity
 TTI Time to Interactivity czas od pierwszego requestu do czasu aż strona jest interaktywna onload w ja
 
