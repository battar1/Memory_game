document.querySelector("button").onclick = () => window.location.reload();
const box = document.querySelector(".box");
const emojis = ["HTML", "HTML", "Bootstrap", "Bootstrap", "JavaScript", "JavaScript", "CSS", "CSS", "Git", "Git", "github", "github"];
let flippedCards = [], matchedCards = [], attempts = 0;

const shuffle_emojis = emojis.sort(() => Math.random() > 0.5 ? 1 : -1);

shuffle_emojis.forEach((emoji, i) => {
let item = document.createElement("div");
item.classList.add("col-3", "bg-primary-subtle", "py-2", "fw-bold", "card");
item.setAttribute("data-tool", emoji);
box.appendChild(item);

item.onclick = function () {
if (flippedCards.length < 2 && !item.classList.contains("flipped") && !matchedCards.includes(item)) {
item.innerHTML = emoji;
item.classList.add("flipped");
flippedCards.push(item);

      if (flippedCards.length === 2) {
        attempts++;
        if (flippedCards[0].dataset.tool === flippedCards[1].dataset.tool) {
          matchedCards.push(...flippedCards);
          flippedCards = [];
          if (matchedCards.length === emojis.length) alert(You Win! Attempts: ${attempts});
        } else {
          setTimeout(() => {
            flippedCards.forEach(card => {
              card.innerHTML = "";
              card.classList.remove("flipped");
            });
            flippedCards = [];
          }, 1000);
        }
      }
    }

};
});
