# Google Login

```
npm install @react-oauth/google@latest
```

```react
import { CredentialResponse, GoogleLogin } from "@react-oauth/google";
import jwt_decode from "jwt-decode";
import { useRouter } from "next/router";
import { useAppDispatch } from "src/redux/hooks";
import { logErrorMessage } from "src/redux/notification";

const debug = require("debug")("app:components:GoogleLogin");

interface DecodedToken {
  aud: string;
  azp: string;
  email: string;
  email_verified: string;
  exp: number;
  family_name: string;
  given_name: string;
  iat: number;
  iss: string;
  jti: string;
  name: string;
  nbf: number;
  picture: "https://lh3.googleusercontent.com/a/AGNmyxaWPAR7wNF2HEEC7DdA8sPCKi99hJpuvBP432Z5SQ=s96-c";
  sub: string;
}

interface GoogleButtonProps {}

GoogleButton.defaultProps = {};


export default function GoogleButton(props: GoogleButtonProps) {
  const dispatch = useAppDispatch();
  const router = useRouter();

  function onSuccess(response: CredentialResponse) {
    debug("Google Login Success", response);
    console.log("L", response);
    if (!response.credential) {
      dispatch(
        logErrorMessage("Failed to fetch google access token", {
          extraData: { response },
        })
      );
      return;
    }

    const decodedToken: DecodedToken = jwt_decode(response.credential);
    debug("DECODED TOKEN", decodedToken);

    const { email, given_name, family_name, name, picture } = decodedToken;

    router.push("/onboarding");
  }

  return (
    <GoogleLogin
      onSuccess={onSuccess}
      onError={() => {
        console.log("Login Failed");
      }}
      // useOneTap
    />
  );
}

```

