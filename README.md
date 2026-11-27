## Configuration MLflow et reproduction du meilleur modèle (Random Forest)

### Lancer le serveur MLflow

Dans un terminal, à la racine du projet :

```bash
mlflow server --backend-store-uri sqlite:///mlflow.db --host 127.0.0.1 --port 5000
```

Laisser ce terminal ouvert, puis ouvrir l'interface sur http://127.0.0.1:5000

### Reproduire l'optimisation

1. Ouvrir `optuna-random-forest.ipynb`
2. Exécuter toutes les cellules dans l'ordre (le `random_state=42` garantit les mêmes splits Train/Validation/Test à chaque exécution)
3. L'étude Optuna (30 trials) optimise le F1-score sur l'ensemble de validation
4. Le meilleur modèle est réentraîné sur Train + Validation, évalué sur Test, et enregistré dans le MLflow Model Registry sous le nom `random_forest_churn`

### Résultats du meilleur modèle (Random Forest)

- Hyperparamètres : n_estimators=131, max_depth=16, min_samples_split=17, min_samples_leaf=9, max_features='log2', class_weight='balanced'
- F1-score (Test) : 0.6339
- Accuracy (Test) : 0.7606
- ROC-AUC (Test) : 0.8402