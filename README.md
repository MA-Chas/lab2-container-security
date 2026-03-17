# Lab 2 container security

## Överskrift
I den här labben arbetade jag med att förstå hur man bygger och analyserar containers ur ett säkerhetsperspektiv. Jag skapade både en sårbar och en härdad Docker‑image, skannade dem med Trivy och genererade en SBOM för att se skillnaderna

## Filer
policies/

screenshots/

Dockerfile.hardened

Dockerfile.vulnerable

app.py

requirements.txt

sbom.json

scan-before.txt

scan-after.txt

Readme.me

## Del 1 – Sårbar image
Jag byggde en enkel app och en sårbar Dockerfile. 
Trivy‑scanningen visade många sårbarheter och resultatet finns i scan-before.txt.
Screenshot finns i screenshots/trivy-before.png.

## Del 2
I denna del skapade jag en härdad Docker‑image genom att använda en slim‑baserad Python‑image, köra som en icke‑root‑användare. Efter att ha byggt imagen skannade jag den med Trivy och såg en tydlig minskning av sårbarheter jämfört med den sårbara versionen. 

## Del 3 – SBOM
Jag genererade en SBOM i CycloneDX-format med Trivy. 
Filen finns i sbom.json.

## Del 4 Gatekeeper och Policy‑Enforcement
Här använde jag Gatekeeper för att testa hur Kubernetes‑policies påverkar deployment. Den osäkra “Bad Pod” blockerades som förväntat, medan den härdade podden godkändes. Detta visar hur policy‑enforcement automatiskt stoppar osäkra resurser och hjälper till att hålla klustret konsekvent och säkert. Screenshots finns i gatekeeper-deny.png och gatekeeper-pass.png. Screenshot finns i screenshots/trivy-after.png.

## Screenshots
<img width="1697" height="453" alt="gatekeeper-deny png" src="https://github.com/user-attachments/assets/1c252ef4-94d2-423a-8770-cfe909007d02" />

<img width="1705" height="73" alt="gatekeeper-pass png" src="https://github.com/user-attachments/assets/e768a9f9-432f-49f9-b19b-ab0637231e8a" />

<img width="1076" height="576" alt="trivy-before" src="https://github.com/user-attachments/assets/13b1d9db-2442-4f03-a134-96912c96b988" />

<img width="1240" height="537" alt="trivy-after" src="https://github.com/user-attachments/assets/878a5611-a309-404d-832a-7fc985c02592" />


## Reflektion
I den här labben lärde jag mig hur mycket container‑säkerhet påverkas av val av base image, paketversioner och att köra som en icke‑root‑användare. Det blev tydligt att en härdad Dockerfile kan minska sårbarheter drastiskt. Jag insåg också varför SBOM är viktigt: det ger en fullständig översikt över alla komponenter i en container, vilket gör det enklare att upptäcka och hantera sårbarheter. Gatekeeper visade hur policy‑enforcement förändrar arbetssättet i Kubernetes genom att automatiskt stoppa osäkra deployment‑försök. Det gör att säkerhet blir en del av själva plattformen och inte något man behöver kontrollera manuellt i efterhand.

