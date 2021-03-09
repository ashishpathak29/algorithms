# algorithms

Prob: Given a list of integers, return the largest product that can be made by multiplying any three integers. 
      For example, if the list is [-10, -10, 5, 2], we should return 500, since that's -10 * -10 * 5.
      
const input = [-10, -10, 5, 2]
const K = 3

const a = findHighest(input, K)
console.log(a)

function findHighest(input, K) {

  const results = []

  for (let i = 0; i < Math.pow(2, input.length); i++) {
    let binary = i.toString(2);    

    //we want to provide leading zeros
    binary = "0".repeat(input.length - binary.length) + binary
    
    const bits = binary.split('').map(e => parseInt(e))
    const bitsAggregatedValue = bits.reduce((acc, curr) => acc + curr, 0)
    
    if (bitsAggregatedValue == K) {
      
      const members = []
      let product = 0

      for (let j = bits.length - 1; j >= 0; j--) {
        if (bits[j] == 1) {
          
          members.push(input[j])

          if (product == 0) {
            product = input[j]
          } else {
            product = product * input[j]
          }
        }
      }

      results.push({
        members,
        product
      })
    }
  }

  let finalResultIndex
  let finalResult

  results.forEach((result, index) => {
    if (!finalResultIndex || (result.product > finalResult.product)) {
      finalResultIndex = index
      finalResult = result
    }
  })

  results.push({maxIndex: finalResultIndex})

  return results
}
