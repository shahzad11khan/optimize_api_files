# OPTIMIZE API AND REUSABLE METHODS FOR GET , PORT , UPDATE AND DELETE

# BASE_URL FILE 
# WORK FOR REACT JS AND ALSO NEXT JS DOT WORRY 😊
// src/api/baseUrl.js

const BASE_URL = "BASEURI";
const IMG_BASE_URL = "BASEURI_FOR_IMAGE;

export { BASE_URL,IMG_BASE_URL};

# END_PINTS FILE
// src/api/endpoints.js

const ENDPOINTS = {
  LOGIN: "/auth/login",
  REGISTER: "/auth/register",
  CONTACT:"/contact",
  GET_JOBS:"/jobs",
  IMG_UPLOAD:"/upload",
  APPLY_JOB:"/applyjob",

};

export default ENDPOINTS;
###################################################################
# AXIOS_INSTANCE FILE
// src/api/axiosInstance.js
import axios from "axios";
import { BASE_URL } from "./baseUrl"; // keep only base url

const axiosInstance = axios.create({
  baseURL: BASE_URL,
  headers: {
    "Content-Type": "application/json",
  },
});

export default axiosInstance;
###################################################################
# API_SERVICES FILE FROM HERE WE CAN HANDLE THE DATA LIKE GET RECORDS AND POST RECORDS 🔥
// src/api/apiService.js
import axiosInstance from "./axiosInstance";
import ENDPOINTS from "./endpoints";

  const apiService = {
  // ✅ Generic GET with params
  get: (url, params = {}) => axiosInstance.get(url, { params }),

  // ✅ Other methods
  post: (url, data) => axiosInstance.post(url, data),
  put: (url, data) => axiosInstance.put(url, data),
  delete: (url) => axiosInstance.delete(url),

  // ✅ Specific APIs with params support
  getUsers: (params = {}) => axiosInstance.get(ENDPOINTS.USERS, { params }),
  getPosts: (params = {}) => axiosInstance.get(ENDPOINTS.POSTS, { params }),
  login: (credentials) => axiosInstance.post(ENDPOINTS.LOGIN, credentials),
  register: (data) => axiosInstance.post(ENDPOINTS.REGISTER, data),


 postContact: (data) => axiosInstance.post(ENDPOINTS.CONTACT, data),
  getJobs: (params = {}) => axiosInstance.get(ENDPOINTS.GET_JOBS, { params }),
// ✅ Image Upload API
  uploadImage: (file) => {
    const formData = new FormData();
    formData.append("image", file);
    return axiosInstance.post(ENDPOINTS.IMG_UPLOAD, formData, {
      headers: { "Content-Type": "multipart/form-data" },
    });
  },
  applyJob: (data) => axiosInstance.post(ENDPOINTS.APPLY_JOB, data),
};

  
export default apiService;
###################################################################
# AT LAST, HOW WE CAN ACCESS THESE API_SERVICE FUNCTION ON JS OR JSX FILES
import apiService from './apis/apiService'; 
const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const res = await apiService.postContact(formData);
      console.log("Contact submitted:", res.data);
      setMsg(res.data.message);
    } catch (err) {
      console.error("Error submitting contact:", err.response?.data || err);
    } 
  };
###################################################################




