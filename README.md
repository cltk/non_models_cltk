# old_norse_models_cltk
Trained taggers, tokenizers, etc. for the CLTK


## POS tagging

### Choice of the corpora
Texts already annotated by researchers were selected because they were in Old Norse written from XII to XIV centuries,
the Golden Age of Old Norse texts : `[Icelandic Parsed Historical Corpus](http://www.linguist.is/icelandic_treebank/Download) (version 0.9, license: LGPL)
Paths to annotated texts are made as you can see below:
``` python
    >>> selected_files = ["1150.firstgrammar.sci-lin.tagged", "1150.homiliubok.rel-ser.tagged",
                      "1210.jartein.rel-sag.tagged", "1210.thorlakur.rel-sag.tagged",
                      "1250.sturlunga.nar-sag.tagged", "1250.thetubrot.nar-sag.tagged",
                      "1260.jomsvikingar.nar-sag.tagged", "1270.gragas.law-law.tagged",
                      "1275.morkin.nar-his.tagged", "1300.alexander.nar-sag.tagged",
                      "1310.grettir.nar-sag.tagged", "1325.arni.nar-sag.tagged",
                      "1350.bandamennM.nar-sag.tagged", "1350.finnbogi.nar-sag.tagged",
                      '1350.marta.rel-sag.tagged']
    >>> selected_data = ["icepahc-v0.9/tagged/"+selected_file for selected_file in selected_files]
```
### Extraction of words and tags
``` python
    >>>> words_tags = []
    >>>> for filename in selected_data:
             words_tags.extend(extract_word_and_tags(filename))
```
The function extract_word_and_tags gets a filename as input and returns the list of (word, tag) of the whole text.
Sentences were not segmented so the POS tagger is not trained completely correctly. However, it does the work.

### Taggers trained with TnT
``` python
    >>>> tagger = tnt.TnT()
    >>>> tagger.train(words_tags)
    >>>> with open(os.path.join("taggers", "pos", "tnt.pickle"), "wb") as f:
             mpck = pickle.Pickler(f)
             mpck.dump(tagger)
```
The model data of the TnT can be retrieved thanks to the pickle module.