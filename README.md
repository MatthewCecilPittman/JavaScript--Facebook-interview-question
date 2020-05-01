# JavaScript--Facebook-interview-question
Daily coding problem Number 19

```
function minCostHouseColor(costs) {

  return minCostHouseColorBest(costs);
}
function minCostHouseColorInitialSolution(costs) {
  if (costs.length === 0) return 0;

  const n = costs.length;
  const k = costs[0].length;

  
  const dp = [...Array(n)].map(() => Array(k));

  
  for (let col = 0; col < k; col++) {
    dp[0][col] = costs[0][col];
  }

  for (let row = 1; row < n; row++) {
    for (let col = 0; col < k; col++) {
      dp[row][col] = Number.MAX_SAFE_INTEGER;

      for (let numCol = 0; numCol < k; numCol++) {
        if (numCol !== col) {
          dp[row][col] = Math.min(
            dp[row][col],
            dp[row - 1][numCol] + costs[row][col]
          );
        }
      }
    }
  }

  let minCost = Number.MAX_SAFE_INTEGER;
  for (let col = 0; col < k; col++) {
    minCost = Math.min(minCost, dp[n - 1][col]);
  }

  return minCost;
}
function minCostHouseColorII(costs) {
  if (costs.length === 0) return 0;

  const n = costs.length;
  const k = costs[0].length;

  const dp1 = []; // the last row
  const dp2 = []; // the current row

  
  for (let i = 0; i < k; i++) {
    dp1[i] = costs[0][i];
  }

  for (let row = 1; row < n; row++) {
    for (let j = 0; j < k; j++) {
      dp2[j] = Number.MAX_SAFE_INTEGER;

      for (let m = 0; m < k; m++) {
        if (m !== j) {
          dp2[j] = Math.min(dp2[j], dp1[m] + costs[row][j]);
        }
      }
    }


    for (let j = 0; j < k; j++) {
      dp1[j] = dp2[j];
    }
  }

  let minCost = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < k; i++) {
    minCost = Math.min(minCost, dp1[i]);
  }
  return minCost;
}
function minCostHouseColorIII(costs) {
  if (costs.length === 0) return 0;

  const n = costs.length;
  const k = costs[0].length;

 
  const dp = [];
  let min1 = 0; 
  let min2 = 0; 

  for (let i = 0; i < n; i++) {
    const oldMin1 = min1;
    const oldMin2 = min2;

    min1 = Number.MAX_SAFE_INTEGER;
    min2 = Number.MAX_SAFE_INTEGER;

    for (let j = 0; j < k; j++) {
      if (dp[j] !== oldMin1 || oldMin1 === oldMin2) {
        dp[j] = oldMin1 + costs[i][j];
      } else {
        dp[j] = oldMin2 + costs[i][j];
      }

      if (min1 <= dp[j]) {
        min2 = Math.min(min2, dp[j]);
      } else {
        min2 = min1;
        min1 = dp[j];
      }
    }
  }
  return min1;
}
function minCostHouseColorBest(costs) {
  if (costs.length === 0) return 0;

  const n = costs.length;
  const k = costs[0].length;

  let min1 = 0;
  let min2 = 0;
  let idx1 = -1;

  for (let i = 0; i < n; i++) {
    let m1 = Number.MAX_SAFE_INTEGER;
    let m2 = Number.MAX_SAFE_INTEGER;
    let idx2 = -1;

    for (let j = 0; j < k; j++) {
      let cost = costs[i][j];
      cost += j === idx1 ? min2 : min1;

      if (cost < m1) {
        m2 = m1;
        m1 = cost;
        idx2 = j;
      } else if (cost < m2) {
        m2 = cost;
      }
    }

    min1 = m1;
    min2 = m2;
    idx1 = idx2;
  }

  return min1;
}

minCostHouseColor;

```
