public class GildedRose {
    public static void updateQuality(Item[] items) {
        for (Item item : items) {
            switch (item.name) {
                case "Aged Brie":
                    updateAgedBrie(item);
                    break;
                case "Sulfuras":
                    // Sulfuras doesn't change in quality
                    break;
                case "Backstage passes":
                    updateBackstagePasses(item);
                    break;
                default:
                    if (item.name.startsWith("Conjured")) {
                        updateConjured(item);
                    } else {
                        updateNormalItem(item);
                    }
                    break;
            }
        }
    }

    private static void updateAgedBrie(Item item) {
        if (item.quality < 50) {
            item.quality++;
        }
        item.sellIn--;
        if (item.sellIn < 0 && item.quality < 50) {
            item.quality++;
        }
    }

    private static void updateBackstagePasses(Item item) {
        if (item.quality < 50) {
            if (item.sellIn <= 0) {
                item.quality = 0;
            } else if (item.sellIn <= 5) {
                item.quality += 3;
            } else if (item.sellIn <= 10) {
                item.quality += 2;
            } else {
                item.quality++;
            }
        }
        item.sellIn--;
    }

    private static void updateConjured(Item item) {
        if (item.quality > 0) {
            item.quality -= 2;
        }
        item.sellIn--;
        if (item.sellIn < 0 && item.quality > 0) {
            item.quality -= 2;
        }
    }

    private static void updateNormalItem(Item item) {
        if (item.quality > 0) {
            item.quality--;
        }
        item.sellIn--;
        if (item.sellIn < 0 && item.quality > 0) {
            item.quality--;
        }
    }
}
