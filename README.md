# How to train Word2Vec for your language...

Nie tylko Polski Word2Vec :)

## Requirements
* nltk >= 1.11.1
* regex >= 2016.6.24
* lxml >= 3.3.3
* numpy >= 1.11.2
* konlpy >= 0.4.4 (Only for Korean)
* mecab (Only for Japanese)
* pythai >= 0.1.3 (Only for Thai)
* pyvi >= 0.0.7.2 (Only for Vietnamese)
* jieba >= 0.38 (Only for Chinese)
* gensim > =0.13.1 (for Word2Vec)
* fastText (for [fasttext](https://github.com/facebookresearch/fastText))
	
## Background / References
* Check [this](https://en.wikipedia.org/wiki/Word_embedding) to know what word embedding is.
* Check [this](https://en.wikipedia.org/wiki/Word2vec) to quickly get a picture of Word2vec.
* Check [this](https://github.com/facebookresearch/fastText) to install fastText.
* Watch [this](https://www.youtube.com/watch?v=T8tQZChniMk&index=2&list=PL_6hBtWGKk2KdY3ANaEYbxL3N5YhRN9i0) to really understand what's happening under the hood of Word2vec.
* Go get various English word vectors [here](https://github.com/3Top/word2vec-api) if needed.

## Work Flow
Quoted from `make_wordvectors.sh`:
```
#### Set your hyper-parameters here ####
############## START ###################
lcode="pl" # ISO 639-1 code of target language. See `lcodes.txt`.
max_corpus_size=1000000000 # the maximum size of the corpus. Feel free to adjust it according to your computing power.
vector_size=300 # the size of a word vector
window_size=5 # the maximum distance between the current and predicted word within a sentence.
vocab_size=20000 # the maximum vocabulary size
num_negative=5 # the int for negative specifies how many “noise words” should be drawn
############## END #####################
echo "step 0. Make `data` directory and move there.`
mkdir data; cd data
echo "step 1. Download the stored wikipedia file to your disk."
wget "https://dumps.wikimedia.org/${lcode}wiki/20170820/${lcode}wiki-20170820-pages-articles-multistream.xml.bz2"
echo "step 2. Extract the bz2 file."
bzip2 -d "${lcode}wiki-20170820-pages-articles-multistream.xml.bz2"
cd ..
echo "step 3. Build Corpus."
python build_corpus.py --lcode=${lcode} --max_corpus_size=${max_corpus_size}
echo "step 4. make wordvectors"
python make_wordvectors.py --lcode=${lcode} --vector_size=${vector_size} --window_size=${window_size} --vocab_size=${vocab_size} --num_negative=${num_negative}
```
Alternatively: 
* STEP 4-2. Run `fasttext.sh` to get fastText word vectors. 

## Forked
Forked from: https://github.com/Kyubyong/wordvectors
