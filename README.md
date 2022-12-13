# Study-Hall-Real-World-College-Math
## Snippet of code to show that inclusion of trans males doesn't affect normality of heights very much

# Number of cis men in random sample
cis_num = 1000

mu_cismale, sigma_cismale = 175, 10 # mean and standard deviation
s_cismale = np.random.normal(mu_cismale, sigma_cismale, cis_num)

## Upperbound, ~2% of a population could be trans https://www.sciencedirect.com/science/article/pii/S0889852919300015
## I had assumed transmale height distribution is akin to that of cis-female
mu_transmale, sigma_transmale = 165, 9
s_transmale = np.random.normal(mu_transmale, sigma_transmale, round(cis_num*0.02))

fix, ax = plt.subplots(figsize=(10,10))

(mu, sigma) = norm.fit(np.concatenate((s_cismale, s_transmale)))

bins = np.linspace(100, 200, 100)
plt.hist([s_cismale,s_transmale], bins, stacked=True, density=True, alpha=0.3)

y_cis = norm.pdf(bins, mu_cismale, sigma_cismale)
l_cis = plt.plot(bins, y_cis, 'g--', linewidth=2, label= 'Cis-only')

y_combined = norm.pdf( bins, mu, sigma)
l_combined = plt.plot(bins, y_combined, 'r:', linewidth=2, label= 'Combined')

plt.legend(loc='upper left', labels=['Cis-only fit','Combined fit','Cis-males','Trans-males'])

plt.show()
