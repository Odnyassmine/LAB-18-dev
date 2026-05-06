📱 ViewModelLiveDataDemoEnrichi

Application Android démontrant la gestion moderne des données avec ViewModel + LiveData (Jetpack) et la différence avec l’approche classique.

🚀 Objectifs
Comprendre pourquoi les données sont perdues lors d’une rotation d’écran
Explorer les limites de onSaveInstanceState()
Maîtriser :
ViewModel (persistance des données)
LiveData (mise à jour automatique de l’UI)
Appliquer l’architecture MVVM
Tester des scénarios réels :
Rotation écran
Changement de thème
Process death
Thread background
🧠 Concepts clés
LifecycleOwner : Activity/Fragment qui possède un cycle de vie
ViewModelStore : stocke les ViewModels
ViewModel : survit aux rotations
LiveData : observable lifecycle-aware
MutableLiveData vs LiveData :
Mutable → modifiable (ViewModel)
LiveData → lecture seule (UI)
setValue() vs postValue() :
setValue → thread principal
postValue → thread background
🏗️ Architecture

MVVM (Model - View - ViewModel)

Activity (View)
    ↓ observe
LiveData
    ↓
ViewModel (logique métier)
⚙️ Configuration
Langage : Java
Minimum SDK : API 24
Jetpack Lifecycle : 2.10.0
📦 Dépendances
def lifecycle_version = "2.10.0"

implementation "androidx.lifecycle:lifecycle-viewmodel:$lifecycle_version"
implementation "androidx.lifecycle:lifecycle-livedata:$lifecycle_version"
🖥️ Interface
Affichage du compteur
Boutons :
➕ INCRÉMENTER
➖ DÉCRÉMENTER
🔄 RÉINITIALISER
🔴 Partie 1 : Version classique (problème)
Variable locale dans Activity :
private int count = 0;
❌ Problèmes :
Perte des données lors de rotation
Gestion manuelle avec onSaveInstanceState
Code peu maintenable
🟢 Partie 2 : Version moderne (solution)
✅ ViewModel
public class CounterViewModel extends ViewModel {
    private final MutableLiveData<Integer> count = new MutableLiveData<>(0);

    public LiveData<Integer> getCount() {
        return count;
    }

    public void increment() {
        count.setValue(count.getValue() + 1);
    }
}
✅ Observation LiveData
viewModel.getCount().observe(this, value -> {
    tvCount.setText(String.valueOf(value));
});
✅ Résultat
Données conservées après rotation ✔️
UI mise à jour automatiquement ✔️
Code propre (MVVM) ✔️
Aucun memory leak ✔️
🧪 Tests réalisés
Test	Résultat
Rotation écran	✅ Données conservées
Changement thème	✅ OK
Process death	⚠️ nécessite SavedStateHandle
Thread background	✅ avec postValue
🔥 Bonus
Background thread
count.postValue(current + 1);
SavedStateHandle (persistance avancée)

Permet de conserver les données même après kill du processus.

📊 Comparaison
Critère	Classique	ViewModel
Rotation	❌	✅
UI auto	❌	✅
Lifecycle-aware	❌	✅
Code propre	❌	✅
🎯 Conclusion

Avec ViewModel + LiveData, on obtient :

✔️ Persistance automatique
✔️ UI réactive
✔️ Architecture moderne (MVVM)
✔️ Code maintenable

C’est la méthode recommandée par Google (Jetpack) et utilisée dans les applications professionnelles.

📸 Aperçu

<img width="462" height="953" alt="lab18" src="https://github.com/user-attachments/assets/4b65bf13-b8f7-48cb-b5be-cacec0de3100" />

<img width="396" height="913" alt="lab18 2" src="https://github.com/user-attachments/assets/3ef859ce-1233-4b92-b5cf-027eb382e073" />

<img width="424" height="907" alt="lab18 3" src="https://github.com/user-attachments/assets/0348d977-040b-4ab8-91ed-40279cdcecd3" />



