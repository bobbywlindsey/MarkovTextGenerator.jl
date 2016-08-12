# MarkovTextGenerator.jl

## Install
```
>
```

## Usage
```
# import text
f = open("mark_twain_books/adventures_of_tom_sawyer.txt")
corpus = readall(f);
# clean text
chars_to_remove = r"[^a-z ]" # I prefer whitelisting chars I want to keep
corpus = clean_corpus(corpus, chars_to_remove);

# create finite Markov model (create more for "tricke-down" effect)
ngram = 2
groupby = "words"
M = get_corpus_frequencies(sub_corpus_clean, ngram, groupby = groupby)
M = tuple(M) # add more Markov models to this tuple

# get unique symbols (by words or by characters)
unique_symbols = unique(split(corpus)) # for words
unique_symbols = unique(split(corpus, "")) # for chars

# choose random ngram set of symbols from text
ϕ = get_phi(corpus, ngram, groupby = groupby)
@show ϕ

num_steps = 200
markov_chain_text = generate_text(ϕ, num_steps, unique_symbols, ngram, M,
								  groupby)
join(markov_chain_text, " ")
```
