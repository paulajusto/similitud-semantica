# Predicció Automàtica de Similitud Semàntica en Frases Catalanes

Aquest projecte implementa un sistema per predir la similitud semàntica entre parelles de frases en català. La tasca consisteix a estimar una puntuació numèrica que indica com de semblants són dues frases (de 0 a 5), utilitzant diverses estratègies de representació i models de regressió i classificació.

## Objectius

- Processar i vectoritzar corpus en català per obtenir representacions semàntiques de les frases.
- Implementar diferents baselines, com la similitud cosinus sobre vectors TF-IDF i One-Hot.
- Construir models supervisats amb embeddings preentrenats (FastText i spaCy).
- Avaluar embeddings contextuals de RoBERTa, tant sense fine-tuning com entrenats específicament per STS.
- Comparar models seqüencials amb atenció respecte a models simples d’agregació.
- Analitzar l’impacte de la dimensionalitat i del fet que els embeddings siguin entrenables o no.
- Experimentar amb classificació de textos sobre el corpus TECLA.

## Requisits d’Embeddings

Per executar correctament els experiments amb embeddings preentrenats de FastText, **cal descarregar i tenir accessibles aquests arxius**:

- `cc.ca.300.vec`: fitxer original de FastText en format `.vec` (vectors en català).
- `model_300d.kv`: versió optimitzada en format Gensim KeyedVectors.

**Important**: assegura’t que aquests fitxers estiguin descomprimits i ubicats al directori de treball del projecte o a la ruta especificada al codi.


## Conjunt de Dades

Els experiments s’han basat principalment en el corpus **STS en català** del projecte AINA, que conté parelles de frases amb puntuacions de similitud. Addicionalment, per la part de classificació, s’ha utilitzat el corpus **TECLA**, que conté oracions etiquetades en diverses categories temàtiques.

## Metodologia

1. **Preprocessament del text**
   - Normalització i neteja de les frases.
   - Tokenització i creació de vocabularis.
   - Càlcul de representacions TF-IDF i embeddings.

2. **Baselines**
   - Similitud cosinus amb vectors agregats (mitjana simple i ponderada TF-IDF).
   - One-Hot Encoding amb vocabulari limitat.
   - Embeddings de spaCy i RoBERTa sense entrenament.

3. **Models supervisats**
   - Regressió neuronal sobre vectors agregats.
   - Model amb sortida basada en càlcul cosinus.
   - Model seqüencial amb embeddings i capa d’atenció.

4. **Models contextuals**
   - RoBERTa sense fine-tuning.
   - RoBERTa fine-tuned per la tasca STS.

5. **Experimentació addicional**
   - Entrenament d’embeddings (aleatoris i preentrenats).
   - Classificació de textos amb embeddings i TF-IDF.

## Resultats

- El millor rendiment s’ha obtingut amb **RoBERTa fine-tuned per STS**, assolint correlacions de Pearson superiors a 0.78.
- Els models amb embeddings preentrenats i fixats (no entrenables) han demostrat ser més estables en corpus petits.
- Les agregacions TF-IDF i el càlcul cosinus han superat els models seqüencials sense fine-tuning.
- La classificació de textos sobre TECLA ha obtingut accuràcies properes al 86–87% amb embeddings de FastText.

## Llibreries i Eines

- Python ≥ 3.8
- TensorFlow
- PyTorch
- transformers
- spaCy (`ca_core_news_md`)
- gensim
- datasets
- scikit-learn
- numpy
- matplotlib

## Estructura del Codi

- **Preprocessament i embeddings**: codi per carregar i vectoritzar les frases.
- **Baselines**: càlcul de similitud cosinus i correlació de Pearson.
- **Models supervisats**: entrenament i comparació de regressions i seqüències.
- **Models contextuals**: inferència amb RoBERTa.
- **Anàlisi de resultats**: generació de gràfiques i comparatives.
- **Classificació TECLA**: experiments de classificació de textos.

## Citacions i Recursos

- [FastText](https://fasttext.cc/)
- [Projecte AINA](https://www.aina.cat/)
- [spaCy](https://spacy.io/)
- [Transformers](https://huggingface.co/)

## Autoria

Pràctica desenvolupada com a part d’un projecte acadèmic d’anàlisi de similitud semàntica i classificació de textos en català.

