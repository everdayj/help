import lombok.Data;
import lombok.NoArgsConstructor;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@Data
@NoArgsConstructor
public class Bcategory {

    public static final Logger log = LoggerFactory.getLogger(Bcategory.class);

    private Integer id = -1;
    private Integer domainId;
    private String name = "";
    private Integer catDomainOrder;
    private String expression = "";
    private String desc = "";
    private Boolean validated = false;

    public void setValidated(boolean validated) {
        this.validated = validated;
    }

    public void setValidated(String value) {
        this.validated = "Y".equalsIgnoreCase(value);
    }

    public String getValidatedString() {
        return this.validated ? "Y" : "N";
    }

    public boolean isValid() {
        return domainId != null && catDomainOrder != null && name != null && !name.trim().isEmpty();
    }

    public int compareByKeyTo(String value) {
        return this.id.compareTo(Integer.valueOf(value));
    }

    public int compareTo(Bcategory other) {
        return this.id.compareTo(other.id);
    }

    public void setKey(Integer key) {
        this.id = (key != null) ? key : -1;
    }

    public Integer getKey() {
        return this.id;
    }

    public String getMessageInfo() {
        return this.name;
    }

    public void setDisplay(String display) {
        this.name = display;
    }

    @Override
    public String toString() {
        return this.name;
    }
}
