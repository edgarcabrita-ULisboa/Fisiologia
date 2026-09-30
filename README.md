Adaptação Fisiológica ao Transporte

Uns gráficos para acompanhar como o VO2max, a frequência cardíaca (HR) e o lactato evoluem ao longo de 10 semanas, com uma mudança de cor na linha a marcar a transição entre um 1º e um 2º período (por padrão, a partir da semana 4/5).

Dados

Os dados estão em Fisiologia_Ebook1 - Folha1.csv, uma linha por semana, com o valor médio e o desvio padrão de cada variável:

Semana, Vo2max, Vo2max (DesvP), HR, HR (DesvP), Lactato, Lactato (DesvP)

Instalar
bash
pip install pandas matplotlib
Código

O truque para a linha mudar de cor sem ficar um espaço a meio é dividir os dados em dois grupos que partilham o ponto de corte:

python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("Fisiologia_Ebook1 - Folha1.csv")



periodo1 = df[df["Semana"] <= 4]
periodo2 = df[df["Semana"] >= 4]  

fig, ax = plt.subplots(figsize=(8, 4.5))

for dados, cor, nome in [(periodo1, "red", "1º período"),
                          (periodo2, "royalblue", "2º período")]:
    ax.errorbar(dados["Semana"], dados["Vo2max"], yerr=dados["Vo2max (DesvP)"],
                color=cor, lw=2, marker="o", ms=4,
                mfc="black", mec="black",
                ecolor="black", elinewidth=1, capsize=3,
                label=nome)

ax.spines['right'].set_visible(False)
ax.spines['top'].set_visible(False)
ax.set_xlim(0, 9.3)
ax.set_xticks(range(0, 10))
ax.set_xlabel("Semana")
ax.set_ylabel("VO2max")
ax.set_title("VO2max\nAdaptação no Transporte")

ax.legend()

plt.tight_layout()
plt.show()

Para o HR e o Lactato é o mesmo código, só trocando "Vo2max" / "Vo2max (DesvP)" pelas colunas correspondentes.

Atenção ao ax.set_ylim: tem de ser ajustado à variável que estás a plotar, senão a linha some do gráfico.

