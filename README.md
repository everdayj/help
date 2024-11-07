import java.io.Serializable;
import java.lang.reflect.Field;

public class DataObject implements Serializable, Cloneable, IData {

    public DataObject() {
    }

    /**
     * Checks if the object is valid. Override in subclasses as needed.
     * @return false as default.
     */
    public boolean isValid() {
        System.out.println("Invalid data -");
        return false;
    }

    /**
     * Compares by key; override as necessary.
     * @param key the key to compare
     * @return comparison result; default is -1.
     */
    public int compareByKeyTo(String key) {
        return -1;
    }

    /**
     * Compares to another object; override as necessary.
     * @param other the other object
     * @return comparison result; default is -1.
     */
    public int compareTo(Object other) {
        return -1;
    }

    /**
     * Sets the key. Override as necessary.
     * @param key the key to set
     */
    public void setKey(Object key) {
        // Override in subclass if needed
    }

    /**
     * Gets the key. Override as necessary.
     * @return the key, default is null.
     */
    public Object getKey() {
        return null;
    }

    /**
     * Gets message information, default is toString().
     * @return message information as String.
     */
    public Object getMessageInfo() {
        return this.toString();
    }

    /**
     * Sets insert information. Override as necessary.
     * @param info information to set
     */
    public void setInsertInfo(Object info) {
        // Override in subclass if needed
    }

    /**
     * Clones the object. Tries to perform a shallow copy.
     * @return a cloned object or the original if cloning fails.
     */
    @Override
    public Object clone() {
        Object clone;
        Class<?> clazz = this.getClass();
        Field[] fields = clazz.getDeclaredFields();

        try {
            if (fields.length > 0) {
                clone = clazz.getDeclaredConstructor().newInstance();
                for (Field field : fields) {
                    field.setAccessible(true);
                    field.set(clone, field.get(this));
                }
            } else {
                clone = super.clone();
            }
        } catch (Exception e) {
            clone = this;
        }
        return clone;
    }

    /**
     * Sets the display value. Override in subclass as necessary.
     * @param display the display object
     */
    public void setDisplay(Object display) {
        // Override in subclass if needed
    }

    @Override
    public String toString() {
        return "DataObject{" +
                "key=" + getKey() +
                '}';
    }
}
