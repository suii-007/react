

const styles = {
  heading: {
    backgroundColor: "aqua",
    textAlign: "center",
    padding: "2rem 0px",
    fontWeight: "bold",
    fontSize: "2rem",
  },
  addItem: {
    backgroundColor: "rgb(251, 253, 249)",
    padding: "1rem",
    marginBottom: "1rem",
  },
  addItemDiv: {
    margin: "1rem 0",
  },
  addItemLabel: {
    display: "block",
    marginBottom: "0.5rem",
  },
  addItemInputSelect: {
    height: "2rem",
    width: "100%",
    padding: "0.5rem",
    marginBottom: "0.5rem",
  },
  btn: {
    border: "none",
    backgroundColor: "green",
    color: "white",
    padding: "10px 15px",
    cursor: "pointer",
    marginTop: "1rem",
  },
  itemList: {
    listStyleType: "none",
    padding: 0,
  },
  item: {
    display: "flex",
    justifyContent: "space-between",
    alignItems: "center",
    padding: "0.5rem",
    borderBottom: "1px solid #ccc",
  },
  footer: {
    position: "fixed",
    bottom: 0,
    left: 0,
    right: 0,
    padding: "2rem 0px",
    textAlign: "center",
    fontSize: "1rem",
    fontWeight: "bold",
    backgroundColor: "yellowgreen",
  },
};

const App = () => {
  const [items, setItems] = useState([]);
  const [name, setName] = useState("");
  const [price, setPrice] = useState("");
  const [quantity, setQuantity] = useState("");

  const addItem = () => {
    if (name.trim() && price.trim() && quantity.trim()) {
      setItems([
        ...items,
        { name, price: parseFloat(price), quantity: parseInt(quantity) },
      ]);
      setName("");
      setPrice("");
      setQuantity("");
    }
  };

  const totalCost = items.reduce(
    (sum, item) => sum + item.price * item.quantity,
    0
  );

  return (
    <div>
      <h1 style={styles.heading}>Grocery Shopping List</h1>
      <div style={styles.addItem}>
        <label style={styles.addItemLabel}>Item Name:</label>
        <input
          type="text"
          style={styles.addItemInputSelect}
          value={name}
          onChange={(e) => setName(e.target.value)}
        />

        <label style={styles.addItemLabel}>Price:</label>
        <input
          type="number"
          style={styles.addItemInputSelect}
          value={price}
          onChange={(e) => setPrice(e.target.value)}
        />

        <label style={styles.addItemLabel}>Quantity:</label>
        <input
          type="number"
          style={styles.addItemInputSelect}
          value={quantity}
          onChange={(e) => setQuantity(e.target.value)}
        />

        <button style={styles.btn} onClick={addItem}>
          Add
        </button>
      </div>
      <ul style={styles.itemList}>
        {items.map((item, index) => (
          <li key={index} style={styles.item}>
            {item.name} - ${item.price.toFixed(2)} x {item.quantity} = $
            {(item.price * item.quantity).toFixed(2)}
          </li>
        ))}
      </ul>
      <h2 style={{ textAlign: "center" }}>
        Total Cost: ${totalCost.toFixed(2)}
      </h2>
      <div style={styles.footer}>Happy Shopping!</div>
    </div>
  );
};

export default App;
