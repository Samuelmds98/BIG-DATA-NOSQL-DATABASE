# RESPOSTAS - TESTE DE MONGODB

## IDENTIFICAÇÃO

**Nome completo:** Samuel Mendes da Silva  
**Matrícula:** 2427964
**Email:** samuelmds16@gmail.com
**Data:** 28/02/2026

---

## QUESTÃO 1 - Consulta Básica com Filtros

### Comando Utilizado
```javascript
// Cole aqui seu comando find()

db.movies.find(
  {
    $and: [
      { genres: { $in: ["Drama"] } },
      { year: { $gte: 2010 } },
      { year: { $lte: 2015 } },
      { "imdb.rating": { $gt: 7.5 } }
    ]
  },
  {
    title: 1,
    year: 1,
    "imdb.rating": 1,
    genres: 1,
    _id: 0
  }
).sort({ "imdb.rating": -1 }).limit(20)

```

### Resultado Obtido
- **Quantidade de documentos encontrados:** 352
- **5 primeiros filmes (título e rating):**
  1. Drishyam 8.9
  2. Most Likely to Succeed 8.9
  3. Kaakkaa Muttai 8.8
  4. Killswitch 8.8
  5. The Great Alone 8.7

### Screenshot
Q1.png

### Observações (opcional)
Como estou conectado via terminal contei usando:
```
db.movies.countDocuments({
  genres: { $in: ["Drama"] },
  year: { $gte: 2010, $lte: 2015 },
  "imdb.rating": { $gt: 7.5 }
})
```
---

## QUESTÃO 2 - Agregação com Agrupamento

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([
  {
    $match: {
      "countries.0": { $exists: true }
    }
  },
  { $unwind: "$countries" },
  {
    $group: {
      _id: "$countries",
      filmes: { $sum: 1 }
    }
  },
  { $sort: { filmes: -1 } },
  { $limit: 10 }
])
```

### Resultado Obtido

| Posição | País | Quantidade de Filmes |
|---------|------|----------------------|

1       | USA        | 10921
2       | UK         | 2652
3       | France     | 2647
4       | Germany    | 1494
5       | Canada     | 1260
6       | Italy      | 1217
7       | Japan      | 786
8       | Spain      | 675
9       | India      | 564
10      | Australia  | 470

### Screenshot
Q2.png

### Observações (opcional)


---

## QUESTÃO 3 - Pipeline com $unwind e $group

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline de agregação
db.movies.aggregate([


])
```

### Resultado Obtido

| Posição | Ator | Qtd Filmes | Rating Médio |
|---------|------|------------|--------------|
1       | Gèrard Depardieu     | 67         | 6.69
2       | Robert De Niro       | 58         | 6.96
3       | Michael Caine        | 51         | 6.71
4       | Bruce Willis         | 49         | 6.41
5       | Samuel L. Jackson    | 48         | 6.40

### Screenshot
Q3.png

### Observações (opcional)

O enunciado pede para considerar apenas filmes que tenham rating definido, então adicionei um $match inicial com $exists: true antes de entrar na pipeline principal. filtrei filmes sem elenco pra não processar documento inútil

---

## QUESTÃO 4 - Agregação com $lookup

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline com $lookup
db.movies.aggregate([


])
```

### Resultado Obtido

**Filme 1:**
- Título: 
- Ano: 
- Quantidade de comentários: 
- Primeiros 3 usuários:
  1. Nome: __________ | Email: __________
  2. Nome: __________ | Email: __________
  3. Nome: __________ | Email: __________

**Filme 2:**
- Título: 
- Ano: 
- Quantidade de comentários: 
- Primeiros 3 usuários:
  1. Nome: __________ | Email: __________
  2. Nome: __________ | Email: __________
  3. Nome: __________ | Email: __________

### Screenshot

Q4.png

### Observações (opcional)

Primeira tentativa foi fazer o $lookup sem filtro previo, travou.
Tentei colocar $limit dentro do $lookup mas não rola, resolvi usando $slice, mas ainda ficou muito ruim.
então a partir dos comments agrupei os filmes. estourou limite de memoria.

---

## QUESTÃO 5 - Agregação com Múltiplos Estágios

### Pipeline Utilizada
```javascript
// Cole aqui sua pipeline completa
db.movies.aggregate([


])
```

### Resultado Obtido

| Gênero | Qtd Filmes | Rating Médio |
|--------|------------|--------------|
| | | |
| | | |
| | | |
| | | |

### Explicação
**Por que esses gêneros são considerados subestimados?**


### Screenshot
_[Anexar screenshot ou indicar arquivo: questao07.png]_

---
