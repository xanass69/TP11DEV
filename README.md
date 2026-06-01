# TP 11 — Localisation d’un smartphone et envoi des coordonnées vers un serveur distant

## Objectifs pédagogiques

| Objectif | Description |
|----------|-------------|
| Récupérer la position GPS | Latitude / Longitude du smartphone |
| Gérer les permissions | Localisation (fine/approximative) + réseau |
| Envoyer les données | Android → PHP via HTTP (Volley / HttpURLConnection) |
| Stockage distant | MySQL |
| Architecture | Projet mobile connecté à un backend |

## Résultat attendu

1. L'utilisateur ouvre l'application  
2. Permission de localisation demandée  
3. Position GPS récupérée  
4. Envoi automatique (ou via bouton) au serveur PHP  
5. Serveur stocke les coordonnées en base MySQL  

2. Dépendances (build.gradle)
gradle
implementation 'com.android.volley:volley:1.2.1'
implementation 'com.google.android.gms:play-services-location:21.0.1'
3. Code Java (activité simplifiée)
Récupération de la position
java
FusedLocationProviderClient client =
    LocationServices.getFusedLocationProviderClient(this);

if (checkSelfPermission(Manifest.permission.ACCESS_FINE_LOCATION) 
        == PackageManager.PERMISSION_GRANTED) {
    client.getLastLocation().addOnSuccessListener(location -> {
        double lat = location.getLatitude();
        double lng = location.getLongitude();
        envoyerAuServeur(lat, lng);
    });
}
