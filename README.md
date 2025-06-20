class SearchSuggestionSystem {
    constructor(products) {
        this.products = products.sort();
    }

    getSuggestions(searchWord) {
        const results = [];
        let prefix = '';
        for (let i = 0; i < searchWord.length; i++) {
            prefix += searchWord[i];
            const startIndex = this.lowerBound(this.products, prefix);
            const suggestions = [];
            for (let j = 0; j < 3; j++) {
                const idx = startIndex + j;
                if (idx < this.products.length && this.products[idx].startsWith(prefix)) {
                    suggestions.push(this.products[idx]);
                } else {
                    break;
                }
            }
            results.push(suggestions);
        }
        return results;
    }

    lowerBound(arr, x) {
        let low = 0;
        let high = arr.length;
        while (low < high) {
            const mid = Math.floor((low + high) / 2);
            if (arr[mid] < x) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        return low;
    }
}
